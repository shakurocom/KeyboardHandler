![Shakuro KeyboardHandler](Resources/title_image.png)
<br><br>
# Keyboard Handler
![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Platform](https://img.shields.io/badge/platform-iOS-lightgrey.svg)
![License MIT](https://img.shields.io/badge/license-MIT-green.svg)

- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

A wrapper around keyboard notifications.

## Requirements

- iOS 10.0+
- Xcode 11.0+
- Swift 5.0+

## Installation

### CocoaPods

To integrate KeyboardHanler into your Xcode project with CocoaPods, specify it in your `Podfile`:

```ruby
pod 'Shakuro.KeyboardHandler'
```

Then, run the following command:

```bash
$ pod install
```

### Manually

If you prefer not to use CocoaPods, you can integrate Shakuro.KeyboardHandler simply by copying it to your project.

## Usage

Have a look at the [KeyboardHandler_Example](https://github.com/shakurocom/KeyboardHandler/tree/main/KeyboardHandlerExample)

Add a strong reference inside your `UIViewController`:

```swift
private var keyboardHandler: KeyboardHandler!
```

Initialize it inside `viewDidLoad()`:

```swift
keyboardHandler = KeyboardHandler(heightDidChange: { [weak self] (newKeyboardHeight: CGFloat, animationDuration: TimeInterval) in
    if let strongSelf = self {
        // animate UI
    }
})
```

It is better to enable and disable it when your controller is appearing and disappering:

```swift
override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    keyboardHandler.isActive = true
}

override func viewDidDisappear(_ animated: Bool) {
    super.viewDidDisappear(animated)
    keyboardHandler.isActive = false
}
```

## iPhone X

On **iPhone X** exists new feature to quickly switch between apps. Quick change between two apps one of which has open keyboard leads to several notifications generated with wrong data. At the moment there is no way to detect these "bad" notifications. So, it is strongly advised to add additional check before you do your animations:

```swift
// inside KeyboardHandler's block
if let strongSelf = self {
    if strongSelf.controlWithKeyboardIsEditing() || newKeyboardHeight == 0 {
        // animate UI
    }
}



// somewhere in your UIViewController
private func controlWithKeyboardIsEditing() -> Bool {
    return someTextField.isEditing   // or some other expression, that suits your needs
}
```

## License

Shakuro.Router is released under the MIT license. [See LICENSE](https://github.com/shakurocom/KeyboardHandler/blob/main/LICENSE.md) for details.

## Give it a try and reach us

Star this tool if you like it, it will help us grow and add new useful things. 
Feel free to reach out and hire our team to develop a mobile or web project for you.
