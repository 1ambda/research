## iPhone Basics

### Xcode 6 Tutorial

[Apple: Xcode 6 Tutorial](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOS/FirstTutorial.html)

### Basics

`Supporting Files` 밑 `main.m` 의 코드는 다음과 같다.

```objective-c
int main(int argc, char * argv[]) {
    @autoreleasepool {
        return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
    }
}
```

`UIApplication` which defined in the **UIKit Framework** called the **appication object**. The application object manages

- the app event loop
- coordinates other high-level app behaviors

`AppDelegate` called **app delegate**

- The app delegate creates the window where your app's content is drawn and provides a place to respond to state transitions within the app.
- The app delegate is where you write your custom app-level code.

### App Delegate

```objective-c
// AppDelegaqte.h
@interface AppDelegate : UIResponder <UIApplicationDelegate>

@property (strong, nonatomic) UIWindow \*window;

@end
```

The app delegate interface contains a single property `window`. With this property the app delegate keeps track of the window in which all of your app content is drawn.

The app delegate implementation contains *skeletons* of important methods. These predefined methods allow the application object to talk to the app delegate. During a significant runtime event for example

- app launch
- low-memory
- app termination

The application object calls the corresponding methods in the app delegate (`AppDelegate.m`), giving it an opportunity to respond appropriately.

### View Controller

![](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOS/Art/view_layer_objects_2x.png)

If your app has multiple content views, you use a different custom view controller class for each content view.

### Action

An action is a piece of code that’s linked to an event that can occur in your app. When that event takes place, the code gets executed.

```objective-c
- (IBAction) restoreDefaults:(id)sender;
```

The sender parameter points to the object that was responsible for triggering the action. The IBAction return type is a special keyword; it’s like the void keyword, but it indicates that the method is an action that you can connect to from your storyboard in Interface Builder (which is why the keyword has the IB prefix).

### Outlets

**Outlets** providee a way to reference interface objects which you added to your story board from source code files.

```objective-c
@property(weak, nonatomic) IBOutlet UITextField *textField;
```

The `IBOutlet` keyword tells Xcode that you can connect to this property from Interface Builder.

### Controls

A control is a user interface object such as a button, slider, or switch that users manipulate to interact with content, provide input, navigate within an app, and perform other actions that you define. Controls enable your code to receive messages from the user interface.

- Touch and drag events
- Editing events
- Value-changed events

### Architecture

![](http://image.slidesharecdn.com/introductiontomvciniphonedevelopment-130405065851-phpapp01/95/introduction-to-mvc-in-iphone-development-10-638.jpg?cb=1422600088)

### synx

[github: synx](https://github.com/venmo/synx)

### ios-good-practices

[iOS Good Practices](https://github.com/futurice/ios-good-practices)

[CocoaPods] manages library dependencies for your Xcode projects.

```
$ sudo gem install cocoapods
$ pod init
$ pod install
$ pod update
```

### Story Board

[스토리보드 기반의 앱 개발](http://www.econovation.co.kr/ecnvb/ios-%EA%B0%9C%EB%B0%9C%ED%8C%81-storyboard-%EA%B8%B0%EB%B0%98%EC%9D%98-%EC%95%B1-%EA%B0%9C%EB%B0%9C/)
