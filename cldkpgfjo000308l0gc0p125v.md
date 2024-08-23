---
title: "My first contribution to scala metals in 2023"
seoTitle: "scala vscode metals"
datePublished: Tue Jan 31 2023 20:41:36 GMT+0000 (Coordinated Universal Time)
cuid: cldkpgfjo000308l0gc0p125v
slug: my-first-contribution-to-scala-metals-in-2023
tags: scala, functional-programming, vscode-extensions, metals

---

## what's metals

metals is the new Scala IDE with supreme support of Scala 3. Killer Features include worksheet :

![](https://docs.scala-lang.org/resources/images/scala3-book/metals-worksheet.png align="left")

that eval code on the air instantly . In my opinion, this way of combining the Haskell REPL and python's jupyter notebook is taking functional programming to the next level of productivity!

Another surprise is that running code like below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675109800678/9380067c-dc3d-42ba-b024-ebdb82336d70.png align="center")

takes only 1s thanks to the incremental compilation, which means it's even more convenient than writing scripts!

However, I find a small annoying thing: when expanding selections in comments, it's too wide so the whole file will be selected:[https://github.com/scalameta/metals/issues/3615#issuecomment-1031257600](https://github.com/scalameta/metals/issues/3615#issuecomment-1031257600),because the presentation compiler ignores comments.

# Into the metals code

It's a bit complicated to navigate the metals codebase,but thanks to the help from active metals developer [Tomasz Godzik](https://github.com/tgodzik) I learned the whole process of testing metals.

# testing

### run test with sbt

It's convenient to test in sbt first. For my case, the relevant file for selection expansion is "SelectionRangeProvider" in subproject "cross", and the command corresponding test is in "cross/testOnly tests.pc.SelectionRangeSuite"(note the cross prefix! otherwise there'll be lots of errors). We can use println or **pprint.log** for debugging,which will also write in the **metals.log** file in .metals folder under project directory when going through manual test later.

### manual test in vscode

After the initial success, It's time to test in the real world!

First, if you didn't change mtags project, then publishLocal is enough. otherwise if you changed mtags(here I only added this feature in for Scala 3 ) :

```plaintext
publishLocal;++3.2.1 mtags/publishLocal
```

"++3.2.1 mtags/publishLocal" is important, otherwise it will take long time to publish for all versions (and also generate lots of errors.. ).

Then, change the user config json in vscode(look for the publish version in previous steps ):

```plaintext
"metals.serverVersion": "0.11.13-SNAPSHOT"
```

Lastly, **restart server** in vscode command palette, and wait for metals to reload and check the metals.log .

## misc

I recommend the below resources to get started:

[https://www.chris-kipp.io/blog/an-intro-to-the-scala-presentation-compiler](https://www.chris-kipp.io/blog/an-intro-to-the-scala-presentation-compiler)

[https://github.com/scalameta/metals/blob/main/architecture.md](https://github.com/scalameta/metals/blob/main/architecture.md)

[https://scalameta.org/metals/docs/contributors/getting-started](https://scalameta.org/metals/docs/contributors/getting-started)

For those who are curious about where's the metals binary, here's the answer from [https://github.com/scalameta/metals/issues/4920](https://github.com/scalameta/metals/issues/4920):

```plaintext
 there is no binary location or anything. It simply puts together the necessary Metals classpath and runs it uses coursier.
```