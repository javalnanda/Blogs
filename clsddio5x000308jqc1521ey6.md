---
title: "SwiftUI View Extensions vs ViewModifier vs Custom Views"
seoTitle: "Customising SwiftUI View"
seoDescription: "Which approach to use when customising SwiftUI View?"
datePublished: Thu Feb 08 2024 15:28:37 GMT+0000 (Coordinated Universal Time)
cuid: clsddio5x000308jqc1521ey6
slug: swiftui-view-extensions-vs-viewmodifier-vs-custom-views
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707413885270/d6bf7bc6-cf4a-4a99-bf3d-4b00d8854c36.png
tags: swift, ios, mobile-development, swiftui

---

We often need to modify the SwiftUI view in some way or the other. There are three ways in which we can achieve customization of the SwiftUI View:

* View Extensions
    
* ViewModifiers
    
* Custom Views
    

We can **almost** produce the same results with the above alternatives, leading to confusion about when to use them. 🤔

**TL;DR:**

* *View Extensions: To apply simple stylings (e.g. colour, padding, etc).*
    
* *ViewModifiers: To apply state-based styling or complex styling(multiple modifiers).*
    
* *Custom Views: For containers, when composing multiple views.*
    

Let's take a simple example of styling the `Text` label to be used as Headers.

Approach 1: Using View extension:

```swift
public extension View {
    func applyHeaderStyle() -> some View {
        lineLimit(1)
        .font(.largeTitle)
        .fontDesign(Font.Design.serif)
    }
}
```

Approach 2: Using ViewModifier:

```swift
struct HeaderLabel: ViewModifier {
    func body(content: Content) -> some View {
        content
            .lineLimit(1)
            .font(.largeTitle)
            .fontDesign(Font.Design.serif)
    }
}
```

Both would give the same result visually if you check the following code in the preview:

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            // Text styled using view extension
            Text("Header Text")
                .applyHeaderStyle()

            // Text styled using view modifier
            Text("Header Text")
                .modifier(HeaderLabel())
        }
    }
}

#Preview {
    ContentView()
}
```

We can further simply the API for accessing `HeaderLabel` modifier by extending the `View` with a function that applies the `.modifier()` . That is how it is demonstrated in Apple's [documentation](https://developer.apple.com/documentation/swiftui/reducing-view-modifier-maintenance) also.

```swift
extension View {
    func headerTextFormat() -> some View {
        modifier(HeaderLabel())
    }
}

// Usage
struct ContentView: View {
    var body: some View {
        VStack {
            // Text styled using view extension
            Text("Header Text")
                .applyHeaderStyle()

            // Text styled using view modifier
            Text("Header Text")
                .headerTextFormat()
        }
    }
}
```

So, what's the difference between Approach 1 and Approach 2?

Visually, there is no difference for this simple customization which does not involve any states. But, we would notice a difference when you try to print the view if required for debugging as follows:

```bash
Type Of TextWithExtension::
 ModifiedContent<ModifiedContent<ModifiedContent<Text, _EnvironmentKeyWritingModifier<Optional<Int>>>, _EnvironmentKeyWritingModifier<Optional<Font>>>, _EnvironmentKeyTransformModifier<Array<AnyFontModifier>>>

Type Of TextWithModifier::
 ModifiedContent<Text, HeaderLabel>  
```

As we can see, when muliple modifiers are applied the view modifier approach encapsulates the internals properly.

I would go for view extensions when applying simple customisation or adding syntactic sugar to existing modifiers as discussed in the previous [blog](https://javalnanda.com/mastering-conciseness-the-art-of-syntactic-sugar-in-code).

ViewModifier is the obvious choice when we want to apply styling based on `@State` . `ViewModifier` can have internal `@State` and it is mostly similar to `View` . Internal states are not possible with extensions. Note, we can still achieve it by passing the binding to the function in the extension but it would be ideal to use ViewModifier.

Suppose we want to allow the user to be able to drag the `Text` label and on release it should move back to its original position. We can define our custom `ViewModifier` in this case as follows:

```swift
import SwiftUI

private struct SpringGesture: ViewModifier {
    @State private var offset: CGSize = .zero

    func body(content: Content) -> some View {
        content
            .offset(x: offset.width, y: offset.height)
            .animation(.interactiveSpring(), value: offset)
            .simultaneousGesture(
                DragGesture()
                    .onChanged { gesture in
                        self.offset = gesture.translation
                    }
                    .onEnded { value in
                        offset = CGSize.zero
                    }
            )
    }
}

private extension View {
    func applySpringGesture() -> some View {
        modifier(SpringGesture())
    }
}

// Usage:
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Drag me")
                .applySpringGesture()
        }
    }
}

#Preview {
    ContentView()
}
```

As we can see in the above example, we need an internal `@State` variable to keep track of `offset`.

Now, this can also be achieved by defining a custom `View` instead of `ViewModifier` . So, when to use custom views then?

If we take a look at SwiftUI's built-in API, containers such as `HStack` `VStack` are views whereas the styling API like `padding` `.background(content:)` are implemented as view modifiers.

So, whenever we are creating container views or creating views where defining its own type makes sence, we can use custom views instead of view modifiers.

For example, if we want to define a view that display's icon along with text:

```swift
import SwiftUI

public struct TextWithIcon: View {
    let icon: Image
    let text: String
    
    public init(
        icon: Image,
        text: String
    ) {
        self.icon = icon
        self.text = text
    }
    
    public var body: some View {
        HStack(alignment: .center, spacing: 4) {
            Text(text)
            icon
                .resizable()
                .renderingMode(.template)
                .frame(width: 16, height: 16)
        }
    }
}

// Usage:
struct ContentView: View {
    var body: some View {
        VStack {
            TextWithIcon(icon: Image(systemName: "swift"), text: "Hello Swift!")
        }
    }
}

#Preview {
    ContentView()
}
```

I hope this examples were helpful and clears the confusion of when to use view extensions, view modifiers and custom views in SwiftUI

Let me know if you found this helpful. Feel free to tweet me on [Twitter](https://twitter.com/javalnanda) if you have any additional tips or feedback.

Thanks