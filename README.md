# awesome-function-builders
A list of cool DSLs made with Swift 5.1’s `@functionBuilder`

> Currently, you instead have to use `@_functionBuilder` as it is a private implementation. This will change in the future, however.

Feel free to contribute if you make or find something awesome.

## Contents

* [The Proposal (SE-XXXX)](https://github.com/apple/swift-evolution/blob/9992cf3c11c2d5e0ea20bee98657d93902d5b174/proposals/XXXX-function-builders.md)

	> The proposal has not been fully implemented in the current Xcode betas, which provide a simpler transformation than specified.

* [Guides](#guides)
* Projects
	* [Dependency Injection](#dependency-injection)
	* [GraphQL](#graphql)
	* [HTML](#html)
	* [Networking](#networking)
	* [NSAttributedString](#nsattributedstring)
	* [REST](#rest)
  * [Server-Side](#server-side)
  * [SwiftUI](#swiftui)
  * [Testing](#testing)
  * [UIKit](#uikit)
  * [Other](#other)

## Guides
A list of helpful guides/tutorials on function builders

* [Crash course in Swift's 'function builders' with SwiftUI](https://blog.vihan.org/swift-function-builders/)
* [Inside SwiftUI's Declarative Syntax's Compiler Magic](https://swiftrocks.com/inside-swiftui-compiler-magic.html?source=post_page---------------------------)
* [The Swift 5.1 features that power SwiftUI’s API](https://www.swiftbysundell.com/posts/the-swift-51-features-that-power-swiftuis-api#function-builders)
* [Create Your First Function Builder in 10 Minutes](https://link.medium.com/8jxUOvuXLY)

## Dependency Injection
* [DependencyInjection](https://github.com/sebastianpixel/DependencyInjection) - Dependency injection with function builders and property wrappers

```swift
DIContainer.register {
  New(MediaPlayer() as MediaplayerProtocol)
  New { _, id in ArticleViewModel(id: id) as PageViewModelProtocol }
  Shared(Router.init, as: RouterProtocol.self, DeeplinkHandler.self)
}
```

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

* [SociableWeaver](https://github.com/NicholasBellucci/SociableWeaver) - Build declarative GraphQL queries in Swift.

```swift
Weave(.query) {
    Object(Post.self) {
        Field(Post.CodingKeys.title)

        Object(Post.CodingKeys.author) {
            Field(Author.CodingKeys.id)
            Field(Author.CodingKeys.name)
                .argument(key: "lastName", value: "Doe")
        }

        Object(Post.CodingKeys.comments) {
            Field(Comment.CodingKeys.id)
            Field(Comment.CodingKeys.content)
        }
        .argument(key: "filter", value: CommentFilter.recent)
    }
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

* [HyperSwift](https://github.com/johngarrett/HyperSwift) - A Swift DSL for generating HTML and CSS documents

```swift
VStack(justify: .center, align: .center) {
  HStack(justify: .spaceEvenly, align: .center) {
    Image(url: "/images/error_bomb.png")
      .width(100)
      .height(100)
    Header(.header3) { "HTTP 500" }
      .font(weight: "bold", size: 40, family: "SF Mono")
  }          
  Paragraph(fiveOfiveMessage)
}
.backgroundColor(GColors.lightRed)
.textAlign(.center)
.margin(5, .percent)
.display(.flex)
.shadow(x: 20, y: 30, color: GColors.cardShadow)
.border(width: 1, color: .black)
```

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

## REST
* [Corvus](https://github.com/apodini/corvus) – Building RESTful APIs with a declarative syntax.

```swift
var api = Api {
    BasicAuthGroup<User>("login") { login }
    JWTAuthGroup<User.Payload> {
        Group("users") { users }
        Group("inventory") {
            Group("articles") { articles }
        }
    }
}
```

* ...

## Server-Side
* [MacroApp](https://github.com/Macro-swift/MacroApp) - A SwiftUI-like, declarative way to setup endpoints for the [MacroExpress](https://github.com/Macro-swift/MacroExpress) SwiftNIO based web framework framework

```swift
@main
struct HelloWorld: App {
  
  var body: some Endpoints {
    Use(logger("dev"), bodyParser.urlencoded())
          
    Route("/admin") {
      Get("/view") { req, res, _ in res.render("admin-index.html") }
      Render("help", template: "help")
    }
      
    Get { req, res, next in
      res.render("index.html")
    }
  }
}
```

* [Meridian](https://github.com/khanlou/Meridian) - A web server written in Swift that lets you write your endpoints in a declarative way

```swift
struct SampleEndpoint: Responder {
    @QueryParameter("sort_direction") 
    var sortDirection: SortDirection = .ascending
    
    @URLParameter(\.id) var userID
    @EnivronmentObject var database: Database
    
    func body() throws {
        JSON(database.fetchFollowers(of: userID, sortDirection: sortDirection))
    }
}

Server(errorRenderer: BasicErrorRenderer()).register {
  SampleEndpoint()
      .on("/api/users/\(\.id))/followers")
}
.environmentObject(Database())
.listen()
```

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

* [SequenceBuilder](https://github.com/andtie/SequenceBuilder) - Allows you to build arbitrary heterogenous sequences without loosing information about the underlying types. It is especially useful for building custom container views in SwiftUI.

```swift
struct EnumerationView<Content: Sequence>: View where Content.Element: View {

    let content: Content

    init(@SequenceBuilder builder: () -> Content) {
        self.content = builder()
    }

    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            ForEach(sequence: content) { (index, content) in
                HStack(alignment: .top) {
                    Text("\(index + 1). ")
                    content
                }
            }
        }
    }
}

// Usage:
EnumerationView {
  Text("Some text")
  VStack {
    ForEach(0..<10, id: \.self) { _ in
      Text("Lorem ipsum dolet.")
    }
  }
  HStack {
    Text("With image:")
    Image(systemName: "checkmark")
  }
}
```

* [SwiftDB](https://github.com/vmanot/SwiftDB) - A type-safe, SwiftUI-inspired wrapper around CoreData

```swift
// Define an Entity:

struct Foo: Entity, Identifiable {
    @Attribute var bar: String = "Untitled"
    
    var id: some Hashable {
        bar
    }
}

// Define a Schema:

struct MySchema: Schema {
    var entities: Entities {
        Foo.self
        Bar.self
        Baz.self
    }
}
```

## Testing

* [Rorschach](https://github.com/q231950/rorschach) - Write Xcode UI Tests BDD style 🤷🏻‍♂️

```swift
expect(in: &context) {
  Given {
    ILearnABitMore()
    IBuildARocket()
  }
  When {
    ILaunchARocket()
  }
  Then {
    ICanSeeTheStars()
  }
}
```

* [SwiftValidation](SwiftValidation) – Declarative way to validate our object.

```swift
try validate(user) {
    validate(\.id).isPositive()
    validate(\.email) {
        isNotEmpty()
        isEmail()
    }
}
```

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

## AppKit
* [MenuBuilder](https://github.com/j-f1/MenuBuilder) - A convenient way to create menus.
```swift
let menu = NSMenu {
  MenuItem("Click me")
    .onSelect { print("clicked!") } 
  MenuItem("Item with a view")
    .view {
      MyMenuItemView() // any SwiftUI view
    }
  SeparatorItem()
  MenuItem("About") {
    // rendered as disabled items in a submenu
    MenuItem("Version 1.2.3")
    MenuItem("Copyright 2021")
  }
  MenuItem("Quit")
    .shortcut("q")
    .onSelect { NSApp.terminate(nil) }
}

// later, to replace the menu items with different/updated ones:
menu.replaceItems {
  MenuItem("New Item").onSelect { print("Hello!") }
}
```

* ...

## Other
* [Pappe](https://github.com/frameworklabs/Pappe) - A Proof of concept embedded interpreted synchronous DSL for Swift.

```swift
let m = Module { name in
    activity (name.Wait, [name.ticks]) { val in
        exec { val.i = val.ticks as Int }
        whileRepeat(val.i > 0) {
            exec { val.i -= 1 }
            await { true }
        }
    }
    activity (name.Main, []) { val in
        cobegin {
            strong {
                doRun(name.Wait, [10])
            }
            weak {
                loop {
                    doRun(name.Wait, [2])
                    exec { print("on every third") }
                    await { true }
                }
            }
            weak {
                loop {
                    doRun(name.Wait, [1])
                    exec { print("on every second") }
                    await { true }
                }
            }
        }
        exec { print("done") }
    }
}
```

* ...
