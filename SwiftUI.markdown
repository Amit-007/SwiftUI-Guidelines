# SwiftUI Style Guide
### Updated for SwiftUI 2.0

This style guide is different from others you may see, because the focus is centered on readability for print and the web. We created this style guide to keep the code in our books, tutorials, and starter kits nice and consistent — even though we have many different authors working on the books.

Our overarching goals are clarity, consistency and brevity, in that order.

## Table of Contents

* [SwiftUI Guidelines](#swiftui-guidelines)
  * [Naming](#swiftui-naming)
  * [Structure](#swiftui-structure)
  * [Modifiers](#swiftui-modifiers)
  * [Component Design Principle](#swiftui-component-design-principle)


## SwiftUI Guidelines

Here are few practices that we specifically follow while Coding in SwiftUI

### SwiftUI Naming

* Naming a View should be accompanied by the keyword View like “HomeView”.
* Model name should same name with the accompanied View like “Home”.

### SwiftUI Structure

* Every View should be accompanied by its own View Model. 
* Always split button action into specific method instead of writing in the same block. 

**Preferred**:

```swift
struct ContentView: View {
    var body: some View {
      Button(action: buttonAction) {
        Text("Hello!")
          .padding()
      }
    .padding()s
  }

  func buttonAction() {
    print("Button Pressed!")
  }
}
```

### SwiftUI Modifiers

* Write modifier on new line instead of writing immediately after "}" brace. 

**Preferred**:

```swift
struct ContentView: View {
    var body: some View {
      Button(action: buttonAction) {
        Text("Hello!")
          .padding()
      }
    .padding()
  }
}
```

**Not Preferred**:

```swift
struct ContentView: View {
    var body: some View {
      Button(action: buttonAction) {
        Text("Hello!").padding()
      }.padding()
  }
}
```

### SwiftUI Component Design Principle

* Always try to design &encaplsulate View with regards to Single Responsibility Principle. It helps to achieve a more modular, testable & customizable component. 

  **Example:** 
  ```
  |DASHBOARD| can have section |POLL VIEW|, and |POLL VIEW| can have its separate view
  So its better to encapsulate |POLL VIEW| from |DASHBOARD| and have it separately.
  ```
* Use ViewModifiers to apply a particluar style to an element to avoid code duplication

  **Preferred**:

  ```swift
     struct ContentView: View {
        @State private var email = ""
        @State private var confirmEmail = ""
            var body: some View {
                VStack {
                  TextField("Email", text: $email)
                    .modifier(EmailTextField())
                  TextField("Confirm Email", text: $confirmEmail)
                    .modifier(EmailTextField())
              }
          }
      }

      struct EmailTextField: ViewModifier {
          func body(content: Content) -> some View {
              content
                .keyboardType(.emailAddress)
                .autocapitalization(.none)
                .disableAutocorrection(true)
                .accessibility(label: Text("Email"))
          }
      }
  }
  ```
  
  **Not Preferred**:

  ```swift
     struct ContentView: View {
        @State private var email = ""
        @State private var confirmEmail = ""
 
            var body: some View {
              VStack {
                  TextField("Email", text: $email)
                    .keyboardType(.emailAddress)
                    .autocapitalization(.none)
                    .disableAutocorrection(true)
                    .accessibility(label: Text("Email"))
                  TextField("Confirm Email", text: $confirmEmail)
                    .keyboardType(.emailAddress)
                    .autocapitalization(.none)
                    .disableAutocorrection(true)
                    .accessibility(label: Text("Email"))
              }
              }
    }
  ```
