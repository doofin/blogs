---
title: "An incomplete guide to Scala 3 macros and Multi-stage programming"
datePublished: Tue Feb 21 2023 20:26:14 GMT+0000 (Coordinated Universal Time)
cuid: cleep5jo300000alc4glid7n7
slug: an-incomplete-guide-to-scala-3-macros-and-multi-stage-programming
tags: scala, metaprogramming, scala3

---

Macros, a form of metaprogramming,or more precisely Multi-stage programming, is a way to modify code as data during compile time. Thanks to this technique, programmers now have the power close to the compiler (although you can't change the syntax arbitrarily), which just also transforms the AST.

As said in Wikipedia, it can be considered as a form of partial evaluation that performs computations at compile-time.To make more analogies, it's also similar to the scenario for embedded DSL, where full access to the AST is given and any transformations are possible.

Mostly based on the official guide at [https://docs.scala-lang.org/scala3/guides/macros/index.html](https://docs.scala-lang.org/scala3/guides/macros/index.html) , I will divide the topic into several parts and focus on theories than giving examples, while also referencing other languages:

* conversion between code and data(AST)
    
* operations on AST (AST for type or terms)
    
* get information from the child node of an AST
    
* organize code and modularity
    

### Clarifying terminologies

* code: the runnable code as it is.
    
* data and AST: we treat the code as data structure. It's usually a tree so we call it AST(abstract syntax tree). Quoted code is a shorthand for manually written AST.
    
* conversion between code and data: usually called
    
    * quote : transform code to data
        
    * splice (or eval) : evaluate data as code
        

### conversion between code and data

Dynamic languages like Lisp(quoted code) and javascript(tostring,eval) make it easy to toggle code and data. In Scala it's different since macros are also statically typed.

The data is called **quoted** code `'{ ... }` (like string "") and the process of converting data back to code is called **splice** `${ ... }`(like ${} inside string). To insert AST(Expr\[T\]) into **quoted** code `'{ ... }`, we can use the syntax $expr or ${ expr }

```scala
import scala.quoted.* // imports Quotes, Expr

def inspectImpl(x: Expr[Any])(using Quotes): Expr[Any] =
  println(x.show)
  x
inline def inspect(inline x: Any): Any = ${ inspectImpl('x) }
```

**inspectImpl** goes from AST to AST as a normal Scala function, while **inline def inspect** has more magic, converting code into AST and invoking inspectImpl.

**using Quotes** contains extra info about Expr\[\_\]. Depending on the desired manipulations for AST(called Expr\[\_\] here), other APIs like **using Type\[T\]** can also be added like below:

```scala
def getTyped[T](x: Expr[T])(using Type[T], Quotes): Expr[T]
```

The Expr.value, Expr.valueOrAbort, and Expr.unapply methods turns the AST Expr to the value(code) if possible.

**Idris Elaborator Reflection:**

In Idris, a dependently typed language, the directive %runElab takes data and turn it into code. The monadic do block of type `Elab a` construct the AST:

```haskell
idNat : Nat -> Nat
idNat = %runElab (do intro `{{x}}
                     fill (Var `{{x}})
                     solve)
```

for more details visit [https://docs.idris-lang.org/en/latest/elaboratorReflection/elaborator-reflection.html#elaborator-reflection](https://docs.idris-lang.org/en/latest/elaboratorReflection/elaborator-reflection.html#elaborator-reflection)

### Operations on AST

**Expr\[t\] and Term**

`Expr[T]` can be seen as wrappers around a `Term` for expressions, where `T` is the statically-known type of the term. Below, we use the extension method asTerm to transform an expression into a term

**Type and TypeRepr**

access type for term : `t.Underlying`

```scala
def evalAndUse[T](x: Expr[T])(using t: Type[T])(using Quotes) = '{
  val x2: t.Underlying = $x // eval AST Expr[T] into x2:T
}
```

Similarly, we can also see Type\[T\] as a wrapper over TypeRepr.

```scala
def f(x: Expr[Int])(using Quotes): Expr[Int] =
  import quotes.reflect.*
  val tree: Term = x.asTerm

def g[T: Type](using Quotes) =
  import quotes.reflect.*
  val tpe: TypeRepr = TypeRepr.of[T]
```

Both Terms and TypeReprs (and therefore Exprs and Types) have an associated symbol, the underlying untyped AST,exposing similar api as java's reflection:

* `declaredFields` and `declaredMethods` : fields ,members and methods inside a class def
    
* `flags` allows you to check multiple properties of a symbol
    
* `companionClass` and `companionModule` jump to and from the companion object/class
    
* `TypeRepr.baseClasses` list of symbols of classes extended by a type, like sealed trait.
    
* `Symbol.pos` the position where the symbol is defined, the source code of the definition, the filename where the symbol is defined,etc
    

## get extra info from AST child node

sometimes we want to get the type of member of a class:

```scala
boxTpe.memberType(leafSym)
```

here we need the parent type **boxTpe** for a child symbol **leafSym.**

More details at [https://docs.scala-lang.org/scala3/guides/macros/best-practices.html](https://docs.scala-lang.org/scala3/guides/macros/best-practices.html)

### Organize code

While working on the AST data structure, the heavy use of path dependent types for type safety adds extra complexity, so more care is needed when referring to types of the AST:

```scala
def getDecls(using Quotes)(rootType: quotes.reflect.TypeRepr) = {
    import quotes.reflect.*
    val typeSybs: Symbol = rootType.typeSymbol
    val decl: List[Symbol] = typeSybs.declarations
  }
```

**quotes** here is not an object, but a method with implicit parameter that can be used in import, which is a huge jump from Scala 2:

```scala
transparent inline def quotes(using inline q: Quotes): q.type = q
```

for keywords **inline** and **transparent,** check [https://docs.scala-lang.org/scala3/guides/macros/inline.html](https://docs.scala-lang.org/scala3/guides/macros/inline.html)

If you want to avoid this fancy **inline transparent** thing:

```scala
  def getDecls(using q: Quotes)(rootType: q.reflect.TypeRepr) = {}
```

## conclusion

In this guide, I provide a more theoretical perspective compared to the official guide while covering less material. Although Scala 3 macros are no longer experimental, it's still a research area and thus under-documented. When combining the new dependent typing, the interaction is nontrivial. In addition, an open problem is: to what extent can we achieve full dependent types with macros?

I recommend the resources below while I'm also trying to understand more about macros :

[https://github.com/nicolasstucki/](https://github.com/nicolasstucki/)

[https://martinfriedrichberger.net/ecoop17.html](https://martinfriedrichberger.net/ecoop17.html)