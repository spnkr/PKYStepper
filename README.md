# PKYStepper [![CocoaPods](https://img.shields.io/cocoapods/v/PKYStepper.svg?style=flat)](http://cocoapods.org/?q=name%3APKYStepper) [![CocoaPods](https://img.shields.io/cocoapods/p/PKYStepper.svg?style=flat)](https://github.com/parakeety/PKYStepper) [![CocoaPods](https://img.shields.io/cocoapods/l/PKYStepper.svg?style=flat)](https://github.com/parakeety/PKYStepper/blob/master/LICENSE)

PKYStepper is a customizable UIControl with stepper and label combined.

<img src="screenshot.png" width="300px;" />

## Requirements
iOS6+


## Features
- block based callback for when value changed, incremented, and decremented
- toggle visibility of increment/decrement button when the value reached its maximun/minimum
- works well with storyboard


## Installation
You can either install using cocoapods(recommended) or copying files manually.

### 1. Cocoapods(Recommended)
In your Podfile, add a line
```ruby
pod 'PKYStepper', '0.0.1'
```
then, run `pod install`.


### 2. Copy files manually

1. Clone this repository
2. Add files under PKYStepper directory to your project


### For objective-c projects
Add `#import 'PKYStepper.h'` in one of your files, and see if your target builds without error.


### For swift projects
You need to create a bridging header and add `#import "PKYStepper.h"` to the header to use the library in swift code.
For instruction on how to create a bridging header, please refer to [Apple's documentation](https://developer.apple.com/library/ios/documentation/swift/conceptual/buildingcocoaapps/MixandMatch.html).


## Usage
### Example
#### Creating PKYStepper by storyboard
Drag `UIView` to your storyboard and change its class to `PKYStepper`. For actual example, take a look at `StoryboardViewController.storyboard` in example project.

```objective-c
@property(nonatomic, weak) IBOutlet PKYStepper *stepper;

- (void)viewDidLoad {
    [super viewDidLoad];
    self.stepper.value = 5.0f;
    self.stepper.stepInterval = 5.0f;
    self.stepper.valueChangedCallback = ^(PKYStepper *stepper, float count) {
        stepper.countLabel.text = [NSString stringWithFormat:@"Count: %@", @(count)];
    };
    [self.stepper setup];
}
```

```swift
@IBOutlet weak var stepper: PKYStepper

override func viewDidLoad() {
  super.viewDidLoad()

  stepper.value = 5.0
  stepper.stepInterval = 5.0
  stepper.valueChangedCallback = { stepper, count in
    stepper.countLabel.text = "Dogs: \(count)"
  }
  stepper.setup()
}
```

#### Creating PKYStepper by code
```objective-c
@property(nonatomic, strong) PKYStepper *stepper;

- (void)viewDidLoad {
  [super viewDidLoad];

  float width = 260.0f;
  float x = ([UIScreen mainScreen].bounds.size.width - width) / 2.0;

  self.stepper = [[PKYStepper alloc] initWithFrame:CGRectMake(x, 100, width, 44)];
  self.stepper.valueChangedCallback = ^(PKYStepper *stepper, float count) {
    stepper.countLabel.text = [NSString stringWithFormat:@"Dogs: %@", @(count)];
  };
  [self.stepper setup];
  [self.view addSubview:self.stepper];
}
```

### Basic Usage
Set a callback and call `setup`.
```objective-c
PKYStepper *stepper = [[PKYStepper alloc] initWithFrame:frame];
stepper.valueChangedCallback = ^(PKYStepper *stepper, float count) {
  stepper.countLabel.text = [NSString stringWithFormat:@"%@", @(count)];
};
[stepper setup];
[self.view addSubview:stepper];
```

```swift
let stepper = PKYStepper(frame: frame)
stepper.valueChangedCallback = { stepper, count in
  stepper.countLabel.text = "\(count)"
}
stepper.setup()
self.view.addSubview(stepper)
```


### Customization
```objective-c
float value; // default: 0.0
float stepInterval; // default: 1.0
float minimum; // default: 0.0
float maximum; // default: 100.0
BOOL hidesDecrementWhenMinimum; // default: NO
BOOL hidesIncrementWhenMaximum; // default: NO
CGFloat buttonWidth; // default: 44.0f

// called when value is incremented
PKYStepperIncrementedCallback incrementCallback;

// called when value is decremented
PKYStepperDecrementedCallback decrementCallback;

// customizing appearance
- (void)setBorderColor:(UIColor *)color;
- (void)setBorderWidth:(CGFloat)width;
- (void)setCornerRadius:(CGFloat)radius;

- (void)setLabelTextColor:(UIColor *)color;
- (void)setLabelFont:(UIFont *)font;

- (void)setButtonTextColor:(UIColor *)color forState:(UIControlState)state;
- (void)setButtonFont:(UIFont *)font;
```


### Further Customization
CountLabel and buttons are exposed as properties, so customize using the properties if you need further control.

