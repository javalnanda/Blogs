---
title: "Mastering Conciseness: The Art of Syntactic Sugar in Code"
seoTitle: "How to write clean code?"
seoDescription: "Adding syntactic sugar to write concise code"
datePublished: Tue Feb 06 2024 09:27:51 GMT+0000 (Coordinated Universal Time)
cuid: clsa5r0r400020al009bkeesb
slug: mastering-conciseness-the-art-of-syntactic-sugar-in-code
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707211750252/51bb8ed7-6bed-4e90-a681-762254124a37.png
tags: software-development, swift, ios, mobile-development, clean-code, swiftui, programming-tips

---

One of the main rules for writing clean code is that it should clearly show what it's meant to do. There are a few things to keep in mind when doing this. It means giving variables and function names that make sense, making sure each part of the code only does one thing without causing other unexpected effects, keeping related code together so it's easier to understand when reading from the top down, etc. For a more detailed guide, I recommend checking out the Clean Code book.

In this blog, I want to talk about how we can make the code we write using the platform's built-in API more straightforward and concise. We often become accustomed to using the platform's native API in a certain way because that's how it's explained in the documentation or tutorials. As a result, we might not realize whether our code is clear or not because it seems obvious to us.

Let's take a look at an example of SwiftUI code below:

```swift
var body: some View {
        VStack {
            // some content
        }
        .frame(maxWidth: .infinity)
    }
```

Can you determine the exact behavior of `.frame(maxWidth: .infinity)` if you're not familiar with SwiftUI? Does it expand to match the width of the parent container? Will it also change the parent container's width, causing it to expand?

  
Now, what about the code below:

```swift
var body: some View {
        VStack {
            // some content
        }
        .fillMaxWidth()
    }
```

Isn't `.fillMaxWidth()` more concise compared to the previous code? The initial code might not be confusing for an iOS developer, but it can be for someone coming from a different platform. I realized this when I was working on both Android and iOS apps, building UI in Jetpack Compose and SwiftUI, respectively. Drawing inspiration from Jetpack Compose, I created syntactic sugar extensions for SwiftUI View. This not only expresses the intent clearly but also reduces verbosity.

```swift
import SwiftUI

public extension View {
  
    func fillMaxSize(alignment: Alignment = .center) -> some View {
        frame(maxWidth: .infinity, maxHeight: .infinity, alignment: alignment)
    }

    func fillMaxWidth(alignment: Alignment = .center) -> some View {
        frame(maxWidth: .infinity, alignment: alignment)
    }

    func fillMaxHeight(alignment: Alignment = .center) -> some View {
        frame(maxHeight: .infinity, alignment: alignment)
    }
}
```

You can find the extension file with additional extensions [here](https://gist.github.com/javalnanda/1f23107bf9a7cd0888c6e3cc99c4d975)

I hope this example helps you look for areas where you can improve the code for more clarity. Looking at other platforms and frameworks also helps us gain a different perspective and draw inspiration from them.

Let me know if you found this helpful. Feel free to tweet me on [Twitter](https://twitter.com/javalnanda) if you have any additional tips or feedback.

Thanks