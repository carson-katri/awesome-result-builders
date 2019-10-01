# awesome-function-builders
A list of cool DSLs made with Swift 5.1’s `@functionBuilder`

> Currently, you instead have to use `@_functionBuilder` as it is a private implementation. This will change in the future, however.  

Feel free to contribute if you make or find something awesome.

## Contents

* [The Proposal (SE-XXXX)](https://github.com/apple/swift-evolution/blob/9992cf3c11c2d5e0ea20bee98657d93902d5b174/proposals/XXXX-function-builders.md)

	> The proposal has not been fully implemented in the current Xcode betas, which provide a simpler transformation than specified.

* [Guides](#guides)
* Projects
	* [GraphQL](#graphql)
	* [HTML](#html)
	* [Networking](#networking)
	* [NSAttributedString](#nsattributedstring)
	* [SwiftUI](#swiftui)
	* [UIKit](#uikit)
	* [Other](#other)

## Guides
A list of helpful guides/tutorials on function builders

* [Crash course in Swift's 'function builders' with SwiftUI](https://blog.vihan.org/swift-function-builders/)
* [Inside SwiftUI's Declarative Syntax's Compiler Magic](https://swiftrocks.com/inside-swiftui-compiler-magic.html?source=post_page---------------------------)
* [The Swift 5.1 features that power SwiftUI’s API](https://www.swiftbysundell.com/posts/the-swift-51-features-that-power-swiftuis-api#function-builders)
* [Create Your First Function Builder in 10 Minutes](https://link.medium.com/8jxUOvuXLY)

## GraphQL
* [Artemis](https://github.com/Saelyria/Artemis) - Interact with GraphQL in Swift - not strings

```swift
Operation(.query) {
  Add(\.country, alias: "canada") {
    Add(\.name)
    Add(\.continent) {
      Add(\.name)
    }
  }.code("CA")
}
```

* [graphique](https://github.com/ilyapuchka/graphique) - Experimental GraphQL query builders

```swift
query("") {
  hero {
    \.name
    lens(\.friends) {
      \.name
    }
  }
}
```

* [Graphiti](https://github.com/GraphQLSwift/Graphiti) - Swift GraphQL Schema/Type framework for macOS and Linux

```swift
Schema<StarWarsAPI, StarWarsStore> {
  Enum(Episode.self) {
    Value(.newHope)
      .description("Released in 1977.")
    Value(.empire)
      .description("Released in 1980.")
    Value(.jedi)
      .description("Released in 1983.")
  }
  .description("One of the films in the Star Wars Trilogy.")
  ...
}
```

* ...

## HTML
* [HTML-DSL](https://github.com/robb/HTML-DSL) - A DSL for writing HTML in Swift

```swift
html(lang: "en-US") {
  body(customData: ["hello":"world"]) {
    article(classes: "readme", "modern") {
      h1 {
        "Hello World"
      }
    }
  }
}
```

* [Vaux](https://github.com/dokun1/Vaux) - A HTML DSL library for Swift

```swift
html {
  body {
    link(url: url, label: "Google", inline: true)
  }
}
```

* ...


## Networking
*  [swift-request](https://github.com/carson-katri/swift-request) - Declarative HTTP networking, designed for SwiftUI

```swift
Request {
  Url("https://jsonplaceholder.typicode.com/todo")
  Header.Accept(.json)
}
.onData { ... }
```
```swift
let myJson = Json {
  JsonProperty(key: "firstName", value: "Carson")
}
myJson["firstName"].string // "Carson"
```

* ...

## NSAttributedString
* [NSAttributedStringBuilder](https://github.com/ethanhuang13/NSAttributedStringBuilder) - Composing NSAttributedString with SwiftUI-style syntax

```swift
NSAttributedString {
  AText("Hello world")
    .font(.systemFont(ofSize: 24))
    .foregroundColor(.red)
  LineBreak()
  AText("with Swift")
     .font(.systemFont(ofSize: 20))
     .foregroundColor(.orange)
}
```

* ...

## SwiftUI
* [ControlFlowUI](https://github.com/Karumi/ControlFlowUI) - A library that add control flow functionality to SwitUI, using the power of `@functionBuilder` and `ViewBuilder`

```swift
List(dogs.identified(by: \.name)) { dog in
  SwitchValue(dog) {
    CaseIs(Animal.self) { value in
      Text(value.species)
    }
    CaseIs(Dog.self) { value in
      Text(value.breed)
    }
  }
}
```

* [PathBuilder](https://github.com/mkj-is/PathBuilder) - Implementation of function builder for SwiftUI Path.

```swift
Path {
  Move(to: CGPoint(x: 50, y: 50))
  Line(to: CGPoint(x: 100, y: 100))
  Line(to: CGPoint(x: 0, y: 100))
  Close()
}
```

* [SwiftWebUI](https://github.com/swiftwebui/SwiftWebUI) - A demo implementation of SwiftUI for the Web

```swift
VStack {
  Text("🥑🍞 #\(counter)")
    .padding(.all)
    .background(.green, cornerRadius: 12)
    .foregroundColor(.white)
    .tapAction(self.countUp)
}
```

* ...

## UIKit
* [BoxLayout](https://github.com/muukii/BoxLayout) - [WIP] SwiftUI's interface like AutoLayout DSL

```swift
BoxCenter {
  BoxVStack {
    BoxElement { toggleView }
    BoxEmpty()
      .frame(height: 20)
    if flag {
      BoxElement { top }
        .aspectRatio(ratio: CGSize(width: 1, height: 1))
    }
  }
}
```

* [LegoKit](https://github.com/octree/LegoKit)

```swift
Lego {
  ForIn(3...4) { x in
    Section(layout:FlowLayout(col: x)) {
      ForIn(0...(x + 3)) { y in
        ImageItem(value: UIImage(named: "\(y % 2)")!)
      }
    }
  }
}
```

* [Mockingbird](https://github.com/DeclarativeHub/Mockingbird) - An experiment of implementing a UI layout and rendering framework inspired by SwiftUI

```swift
var content: some Node {
  VerticalStack {
    Repeated(0..<count) {
      Button(action: { self.count += 1 }) {
        BoxedText()
      }
    }
  }
  .cornerRadius(20)
  .animation(.spring)
}
```

* [TurtleBuilder](https://github.com/zonble/TurtleBuilder) - Turtle graphics made on the top of Swift's function builder. It allows you to use a Logo-like syntax to create and draw lines in your Swift project.

```swift
let turtle = Turtle {
  penDown()
  loop(9) {
      left(140)
      forward(30)
      left(-100)
      forward(30)
  }
  penUp()
}
```

* ...

## Other
* ...
