# Codemine

[![CircleCI](https://circleci.com/gh/nodes-ios/Codemine.svg?style=shield)](https://circleci.com/gh/nodes-ios/Codemine)
[![Codecov](https://img.shields.io/codecov/c/github/nodes-ios/Codemine.svg)](https://codecov.io/github/nodes-ios/Codemine)
[![CocoaPods](https://img.shields.io/cocoapods/v/Codemine.svg)](https://cocoapods.org/pods/Codemine)
[![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
![Swift Package Manager](https://img.shields.io/badge/SPM-compatible-brightgreen.svg)
![Plaform](https://img.shields.io/badge/platform-iOS-lightgrey.svg)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/nodes-ios/Codemine/blob/master/LICENSE)
[![Readme Score](http://readme-score-api.herokuapp.com/score.svg?url=nodes-ios/codemine)](http://clayallsopp.github.io/readme-score?url=nodes-ios/codemine)

Codemine is a collection of extensions containing useful functions and syntactic sugar for your Swift project.


## 📝 Requirements

* iOS 8.0+
* Swift 3.0+


## 📦 Installation

### CocoaPods

If you are using CocoaPods add this text to your Podfile and run `pod install`.
~~~
pod 'Codemine', '~>1.0.0'

# Swift 2.3
pod 'Codemine', '~>0.2.5'

# Swift 2.2
pod 'Codemine', '~>0.2.2'
~~~

### Carthage
~~~
github "nodes-ios/Codemine" ~> 1.0

# Swift 2.3
github "nodes-ios/Codemine" == 0.2.5

# Swift 2.2
github "nodes-ios/Codemine" == 0.2.2
~~~


## 💻 Usage

### Application
```swift
let appName = Application.name             // CFBundleDisplayName : String
let appVersion = Application.version       // CFBundleShortVersionString : String
let appExecutable = Application.executable // CFBundleExecutable : String
let appBundle = Application.bundle         // CFBundleIdentifier : String
let appSchemes = Application.schemes       // CFBundleURLSchemes : [String]
let mainAppScheme = Application.mainScheme // CFBundleURLSchemes.first : String?
```

Gain easy access to main bundle information.

### CGPoint
```swift
let point1 = CGPoint(x: 5, y: 5)
let point2 = CGPoint(x: 5, y: 6)
print(point1.isCloseTo(point2, tolerance: 1))	// true
print(point1.isCloseTo(point2, tolerance: 0.5))	// false
print(point1+point2)	// (10, 11)
print(point1*point2)	// (25, 30)
print(point1*2)			// (10, 10)
print(point1-point2)	// (0, -1)
print(point1/point2)	// (1, 0.83)
print(point1/5)			// (1, 1)
```

### CGRect
```swift
var rect = CGRect(x: 10, y: 10, width: 120, height: 100)
rect.x = 50
print(rect)	// outputs x:50, y:20, width: 120, height:100
rect.y = -10
print(rect)	// outputs x:50, y:-10, width: 120, height:100
let reversedRect = rect.reversingSize
print(reversedRect)	// outputs x:50, y:-10, width:100, height:120
```

### CGSize
```swift
let size1 = CGSize(width: 20, height: 40)
let size2 = CGSize(width: 121, height: 576)
print(size1+size2)		// CGSize(width: 141, height: 616)
```


### NSError
```swift
let error = NSError(domain: domain, code: code, description: description)
```
instead of

```swift
let error = NSError(domain: domain, code: code, userInfo: [NSLocalizedDescriptionKey : description])
```

### NSURL
```swift
guard let url = NSURL(string: "https://example.com/image.png") else { return }
let size = CGSize(width: 512, height: 256)
let heightParameterName = "height"
let widthParameterName = "width"

let url2 = url.appendingAssetSize(size, mode: .default, heightParameterName: heightParameterName, widthParameterName: widthParameterName)
print(url2.absoluteString)	// on an @2x screen: "https://example.com/image.png?width=1024&height=512"
```
This method appends the `size` multiplied by `UIScreen.main.scale` to an asset url so that the asset has the correct size to be shown on the screen.

### String
```swift
let camelCaseStr1 = "userId"
let camelCaseStr2 = "isUserActiveMemberOfCurrentGroup"

print(camelCaseStr1.camelCaseToUnderscore())	// "user_id"
print(camelCaseStr2.camelCaseToUnderscore())	// "is_user_active_member_of_current_group"
```
```swift
"email@example.com".isValidEmailAddress()	// true
"email.example.com".isValidEmailAddress()	// false
```

```swift
let str = "Hello world!"
let range = str.range(from: "e", toString: " w")	// Range(1..<7)
```

### UIColor

```swift
let red = UIColor(rgb: 0xFF0000)
```

### UIImage

```swift
let image = UIImage(color: UIColor.red, CGSize(width: 512, height: 256), cornerRadius:4.0)
```
Returns a `UIImage` filled with red color, of the specified size and with the specified corner radius

```swift
let image = UIImage.embed(icon: UIImage(named:"favouriteIcon"), inImage: UIImage(named:"profilePhoto"))
```
Returns a `UIImage` composed by overlaying the icon on top of the first image.

### UIView
```swift
let view = UIView.from(nibWithName("customView"))
```
Returns a view instantiated from the specified nib.

```swift
let view = UIView(frame: CGRect(x: 0, y: 0, width: 20, height: 20))
view.roundViewCorners(UIRectCorner.allCorners, radius: 4.0)
```
Rounds the specified corners of a `UIView` to the specified radius.

### Then

```
let UIView().then {
  $0.backgroundColor = UIColor.black
}
```

### DispatchTime

```
DispatchQueue.main.asyncAfter(deadline: 5) { /* ... */ }
```

## 👥 Credits
Made with ❤️ at [Nodes](http://nodesagency.com).

`Application` and `Then` were borrowed from Hyper's [Sugar](https://github.com/hyperoslo/Sugar) 🙈.

The `DispatchTime` extensions are [Russ Bishop's idea](http://www.russbishop.net/quick-easy-dispatchtime) 🙈.

## 📄 License
**Codemine** is available under the MIT license. See the [LICENSE](https://github.com/nodes-ios/Codemine/blob/master/LICENSE) file for more info.
