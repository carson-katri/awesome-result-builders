# awesome-result-builders
A list of cool DSLs made with Swift 5.4’s `@resultBuilder`

> As of Swift 5.4, `functionBuilder` has been [renamed to `resultBuilder`](https://github.com/apple/swift-evolution/blob/main/proposals/0289-result-builders.md#changes-from-the-first-revision)

Feel free to contribute if you make or find something awesome.

## Contents

* [The Proposal (SE-0289)](https://github.com/apple/swift-evolution/blob/main/proposals/0289-result-builders.md)

* [Guides](#guides)
* Projects
	* [Data](#data)
	* [Dependency Injection](#dependency-injection)
	* [GraphQL](#graphql)
	* [HTML](#html)
	* [Parsing/Decoding](#parsing-and-decoding)
	* [Networking](#networking)
	* [NSAttributedString](#nsattributedstring)
	* [REST](#rest)
    * [Server-Side](#server-side)
    * [SwiftUI](#swiftui)
    * [Testing](#testing)
    * [UIKit](#uikit)
    * [Other](#other)

## Guides
A list of helpful guides/tutorials on result builders

* [Crash course in Swift's 'function builders' with SwiftUI](https://blog.vihan.org/swift-function-builders/)
* [Inside SwiftUI's Declarative Syntax's Compiler Magic](https://swiftrocks.com/inside-swiftui-compiler-magic.html)
* [The Swift 5.1 features that power SwiftUI’s API](https://www.swiftbysundell.com/posts/the-swift-51-features-that-power-swiftuis-api#function-builders)
* [Create Your First Function Builder in 10 Minutes](https://link.medium.com/8jxUOvuXLY)

## Data
* [BitWiser](https://github.com/DrAma999/BitWiser) - A simple library to help you in dealing with bytes, bits, nibbles and Data

```swift
Data {
  [UInt8(0)]
  UInt8(1)
  Int8(2)
  "\u{03}"
  Int16(1284)
  if dataClause {
    CustomData()
  }
}
    
Array<Byte> {
  0b1010_1010
  0b1100_1100
  UInt8(32)
  [0x05, 0x06]
  Byte(0x01)
}
```

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

* [Mongrel](https://github.com/NicholasBellucci/Mongrel) - Build declarative HTML in Swift.

```swift
struct IndexPage: HTML {
  var body: some HTMLConvertible {
    Root(language: .en) {
      Body {
        Group {
          Text("Welcome to Mongrel!")
            .heading(.h1)

          Text("A Swift and HTML hybrid supporting:")

          List(.unordered) {
            Text("CSS")
              .paragraph()

            Text("Javascript")
              .paragraph()
          }
          .class("list")
        }
      }
      .id("main-body")
    }
  }
}
```

* [Swep](https://github.com/Alja7dali/swift-web-page) - Writing type-safe HTML/CSS declaratively.

```swift
let titillimFont: StaticString = """
  https://fonts.googleapis.com/css2?family=\
  Titillium+Web:ital,wght@0,200;0,300;0,400;\
  0,600;0,700;0,900;1,200;1,300;1,400;1,600;\
  1,700&display=swap
  """
let page = document {
  html {
    head {
      title("Hello, Swep!")
      style {
        `import`(titillimFont)
        selector("*, *::before, *::after") {
          margin(0)
          padding(0)
        }
        selector("body") {
          margin(0, .auto)
          backgroundColor(.hex(0x111))
          fontFamily("'Titillium Web', sans-serif")
        }
      }
    }
    body {
      h1("📄 swift-web-page (swep)")
      ul {
        li("Write html documents along with css")
          .fontWeight(.bolder)
        li("Bring all swift-language features out of the box")
        #if swift(>=5.1)
          for version in 1...4 {
            if version != 2 {
              li("supporting swift v5.\(version)")
            }
          }
        #endif
      }
      blockquote("Enjoy! ✌️😁")
    }
  }
}
```

* ...

## Parsing and Decoding
* [HTMLParserBuilder](https://github.com/danny1113/html-parser-builder) - Build your HTML parser with declarative syntax and strongly-typed result.

```swift
struct Group {
    let h1: String
    let h2: String
}

let capture = HTML {
    Capture("#group h1", transform: \.textContent)
    Capture("#group h2", transform: \.textContent)
    
} transform: { (output: (String, String)) -> Group in
    return Group(
        h1: output.0,
        h2: output.1
    )
} // => HTML<Group>
```

* [DeepCodable](https://github.com/MPLew-is/deep-codable) - Encode and decode deeply-nested data into flat Swift objects

```swift
struct SomeObject: DeepCodable {
    static let codingTree = CodingTree {
        Key("a", "b", "c") {
            Key("d1", "e1", containing: \._e1)
            Key("d2", "e2", "f2", containing: \._f2)
        }
    }
    
    @Value var e1: String
    @Value var f2: String
}

let json = """
    {
        "a": {
            "b": {
                "c": {
                    "d1": {
                        "e1": "Some value"
                    },
                    "d2": {
                        "e2": {
                            "f2": "Other value"
                        }
                    }
                }
            }
        }
    }
    """
let jsonData = json.data(using: .utf8)!

let object = try JSONDecoder().decode(SomeObject.self, from: jsonData)
print(object.e1) // "Some value"
print(object.f2) // "Other value"
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

* [VaporDSL](https://github.com/danny1113/vapor-dsl) - Declarative, structured syntax for Vapor.

```swift
Group("api") {
    // GET /api/
    Route(use: index)
    
    // GET /api/todos
    Route("todos") { req in
        return req.view.render("todos")
    }

    // POST /api/todos
    Route("todos", on: .POST, use: todo)
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

* [ComposableNavigator](https://github.com/Bahn-X/swift-composable-navigator) - The **ComposableNavigator** is based on the concept of PathBuilder composition in form of a NavigationTree. A NavigationTree composes PathBuilders to describe all valid navigation paths in an application. That also means that all screens in our application are accessible via a pre-defined navigation path.

```swift
struct AppNavigationTree: NavigationTree {
  let homeViewModel: HomeViewModel
  let detailViewModel: DetailViewModel
  let settingsViewModel: SettingsViewModel

  var builder: some PathBuilder {
    Screen(
      HomeScreen.self,
      content: {
        HomeView(viewModel: homeViewModel)
      },
      nesting: {
        DetailScreen.Builder(viewModel: detailViewModel),
        SettingsScreen.Builder(viewModel: settingsViewModel)
      }
    )
  }
}
```
Based on `AppNavigationTree`, the following navigation paths are valid:
```
  /home
  /home/detail?id=0
  /home/settings
```

More information on the `NavigationTree` and how to compose `PathBuilder`s can be found [here](https://github.com/Bahn-X/swift-composable-navigator/wiki/NavigationTree).

## Testing

* [Rorschach](https://github.com/q231950/rorschach) - Write XCTest tests in BDD style 🤷🏻‍♂️

```swift
expect {
  Given("I have a universe without any stars") {
      universe.numberOfStars = 0
  }
  When("I add a couple of stars") {
      universe.numberOfStars = 23
  }
  Then("I can see the stars I have added ✨") {
      XCTAssertEqual(universe.numberOfStars, 23)
  }
}
```

* [SwiftValidation](https://github.com/artbobrov/SwiftValidation) – Declarative way to validate our object.

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

* [FlooidLayout](https://github.com/martin-lalev/FlooidLayout) - Setup autolayout constraints in a declerative way

```swift
image.constraints { view in
    view.centerXAnchor == container.centerXAnchor
    view.topAnchor == container.topAnchor + 20
    view.widthAnchor == container.widthAnchor -- 20
    view.heightAnchor == view.widthAnchor * 0.6
}
icon.constraints { view in
    view.centerAnchor == iconContainer.centerAnchor
    view.sizeAnchor == CGSize(width: 20, height: 20)
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

* [SyntaxBuilder](https://github.com/akkyie/SyntaxBuilder) - A *toy* Swift code generator based on SwiftSyntax

```swift
import SyntaxBuilder

struct UserSourceFile: SourceFile {
    let idType: Type

    @SyntaxListBuilder
    var body: Body {
        Import("Foundation")

        Struct("User") {
            Typealias("ID", of: idType)

            Let("id", of: "ID")
                .prependingComment("The user's ID.", .docLine)

            Let("name", of: "String")
                .prependingComment("The user's name.", .docLine)

            Var("age", of: "Int")
                .prependingComment("The user's age.", .docLine)

            ForEach(0 ..< 3) { i in
                Let("value\(i)", of: "String")
                    .prependingNewline()
            }
        }
        .prependingComment("""
            User is an user.
            <https://github.com/akkyie/SyntaxBuilder/>
        """, .docBlock)
    }
}
```

* [Narratore](https://github.com/broomburgo/Narratore) - A library to generate interactive stories and narrative games, that uses a DSL to write the story.

```swift
import Narratore

struct MyFirstScene: Scene {
  typealias Game = MyGame
  
  static let branches: [RawBranch<MyGame>] = [
    Main.raw,
  ]
  
  enum Main: Branch {
    typealias Anchor = String

    @BranchBuilder<Self>
    static func getSteps(for _: MyFirstScene) -> [BranchStep<Self>] {
      "Welcome"
      
      "This is your new game, built with narratore".with(tags: [.init("Let's play some sound effect!")])
      
      check {
        if $0.world.isEnjoyable {
          "Enjoy!"
        }
      }
      
      "Now choose".with(anchor: "We could jump right here from anywhere")
      
      choose { _ in
        "Go to second scene, main path".onSelect {
          "Let's go to the second scene!"
            .with(id: "We can keep track of this message")
            .then(.transitionTo(MySecondScene.init(magicNumber: 42)))
        }

        "Go to second scene, alternate path".onSelect {
          "Going to the alternate path of the second scene"
            .then(.transitionTo(MySecondScene.Other.self, scene: .init(magicNumber: 43)))
        }
      }
    }
  }
}
```
