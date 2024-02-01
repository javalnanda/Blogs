---
title: "How to use Xcode Code Snippet Library?"
seoTitle: "Xcode Code Snippet Library"
seoDescription: "How to use xcode code snippet library"
datePublished: Sun Apr 30 2017 09:45:50 GMT+0000 (Coordinated Universal Time)
cuid: clrs275hj000309le3wnrcvo1
slug: how-to-use-xcode-code-snippet-library-8cd621028f0b
canonical: https://medium.com/faodail-technology/how-to-use-xcode-code-snippet-library-8cd621028f0b
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706165851071/9ca3cbcb-9fce-44b8-b19a-3b1f863eb7a6.png
tags: xcode, ios, mobile-app-development, tips

---

Xcode Code Snippet Library is very useful and handy library of reusable code snippets.

For developers who are starting out iOS development and yet to explore all the features of Xcode, this article is for you.

Xcode Code Snippet Library is accessible from the second tab beside the Object Library from where we grab all the UI components to drag and drop on Storyboard.

It already has some pre-defined code snippets which you can simply drag and drop on your source code and use it by editing as per your needs. You can search for available snippets from the Filter search bar available at the bottom of the library.

For e.g You can use a predefined snippet for swift for statement from the library as shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706116173020/9db69ef5-8f78-46d5-b2e3-2c31273c92b7.gif align="left")

predefined code snippet from library

Pretty hand right? But it is not just limited to predefined snippets available in the library. You can define your own code snippet and save it inside this library.

For e.g the most used snippets we might need are table view delegate methods. Let us see how we can add them to a library:

[**Adding custom code snippet to Xcode snippet library**  
*Edit description*screencast-o-matic.com](http://screencast-o-matic.com/watch/cbfblwXhB4)

As seen in above video, you can simply drag and drop the snippet on Xcode Code Snippet Library and it will prompt a window to add a name for your snippet and there you go. You created your own custom snippet to reuse later.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706116174982/2b386f7f-2998-437d-8572-966873280762.gif align="left")

Wait! There is more to it :\] Did you notice there were few other fields when you gave a name for your code snippets?

![](https://cdn-images-1.medium.com/max/800/0*G4QB7FtZVuUIapR9.png align="left")

Double click on the snippet you just created and go to edit mode. You will see the window same as above screenshot. Here you can add more information like the summary, platform(ios, macOS, etc), Completion Shortcut and Completion Scopes.

**Completion Shortcut:**

This will help you to autocomplete your code snippet without the need of drag and drop from the library. Completion Scopes define where the completion shortcut will work. Let us see this in action based on values I have set as per above screenshot.

![](https://cdn-images-1.medium.com/max/800/1*3b9JMBDdhpgSf1Ck5MJP8A.gif align="left")

snippet auto-completion

As you can see, I defined the completion shortcut within Class Implementations Scope hence it is not available at Top Level scope but can be easily accessed at the class level.

If you find this useful, share with other fellow developers and spread the knowledge 🙂

Happy Coding!