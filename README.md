# NightThemeDemo
A demo project reprinted from raywenderlich website, which demonstrates you how you can configure a Night Theme in iOS App.

![最终效果](http://upload-images.jianshu.io/upload_images/1334681-28ed7d5c166a5f23.gif?imageMogr2/auto-orient/strip)

### 要求：
- Platform: iOS8.0+
- Language: Swift3.2
- Editor: Xcode8+

##### UIApplication Key Window
```
// 主色
UIApplication.shared.delegate?.window??.tintColor = mainColor
```

### UINavigaitonBar
- 导航栏的样式`barStyle`有2中: `default`和`black`，default情况下，status bar的颜色为black，black情况下为white；

![barStyle = .default](http://upload-images.jianshu.io/upload_images/1334681-6c5782d63c4cdabf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![barStyle = .black](http://upload-images.jianshu.io/upload_images/1334681-904e9740bee2bffb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- `black`样式适用于在设置了barTintColor为非黑色的实色的导航栏上；
- 设置导航栏统一的默认返回按钮icon时，要注意设置其`mask`icon为如下样式：

![backIndicatorImage](http://upload-images.jianshu.io/upload_images/1334681-1ca9b00f2358f417.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![backIndicatorTransitionMaskImage](http://upload-images.jianshu.io/upload_images/1334681-77ef3b565971f49e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- mask图组合原理：

![正确的backIndicatorImage和backIndicatorTransitionMaskImage组合模式](http://upload-images.jianshu.io/upload_images/1334681-db119380383144e2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
INavigationBar.appearance().barStyle = barStyle
UINavigationBar.appearance().setBackgroundImage(navigationBarBackgroundImage, for: .default)
UINavigationBar.appearance().backIndicatorImage = UIImage(named: "backArrow")
UINavigationBar.appearance().backIndicatorTransitionMaskImage = UIImage(named: "backArrowMaskFixed")
```
##### UITaBar
- tab bar的`barStyle`和导航栏的显示一样；
- 可以设置tab选中的指示图`selectionIndicatorImage`；

![selectionIndicatorImage](http://upload-images.jianshu.io/upload_images/1334681-301574865bb29a47.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
UITabBar.appearance().barStyle = barStyle
UITabBar.appearance().backgroundImage = tabBarBackgroundImage
let tabIndicator = UIImage(named: "tabBarSelectionIndicator")?
	.withRenderingMode(.alwaysTemplate)
	.resizableImage(withCapInsets: .init(top: 0, left: 2, bottom: 0, right: 2))
UITabBar.appearance().selectionIndicatorImage = tabIndicator
```
##### UISegmentedControl
- 主要是默认背景图的和选中背景图的设置`setBackgroundImage()`；
- 也可以设置某个item的图片`setImage(, forSegmentAt:)`；

![UISegmentedControl](http://upload-images.jianshu.io/upload_images/1334681-e73d12383fac9ec0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
let controlBgImage = UIImage(named: "controlBackground")?
	.withRenderingMode(.alwaysTemplate)
	.resizableImage(withCapInsets: .init(top: 3, left: 3, bottom: 3, right: 3))
let controlSelectedBgImage = UIImage(named: "controlSelectedBackground")?
	.withRenderingMode(.alwaysTemplate)
	.resizableImage(withCapInsets: .init(top: 3, left: 3, bottom: 3, right: 3))
UISegmentedControl.appearance().setBackgroundImage(controlBgImage, for: .normal, barMetrics: .default)
UISegmentedControl.appearance().setBackgroundImage(controlSelectedBgImage, for: .selected, barMetrics: .default)
```
##### UIStepper
- 主要可以设置`normal`、`disabled`和`highlighted`的背景图`setBackgroundImage()`；
- 可以设置加减按钮的图片`setIncrementImage()`和`setDecrementImage()`；

![UIStepper](http://upload-images.jianshu.io/upload_images/1334681-a66590d7309b897e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
let controlBgImage = UIImage(named: "controlBackground")?
	.withRenderingMode(.alwaysTemplate)
	.resizableImage(withCapInsets: .init(top: 3, left: 3, bottom: 3, right: 3))
UIStepper.appearance().setBackgroundImage(controlBgImage, for: .normal)
UIStepper.appearance().setBackgroundImage(controlBgImage, for: .highlighted)
UIStepper.appearance().setBackgroundImage(controlBgImage, for: .disabled)
UIStepper.appearance().setDecrementImage(UIImage.init(named: "fewerPaws")!, for: .normal)
UIStepper.appearance().setIncrementImage(UIImage.init(named: "morePaws")!, for: .normal)
```
##### UISlider
- 主要可以设置拇指按钮的图片`setThumbImage()`；
- 主要可以设最大/最小轨道的图片`setMaximumTrackImage()`和`setMinimumTrackImage()`；

![UISlider](http://upload-images.jianshu.io/upload_images/1334681-d38e5f36d9e26682.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
UISlider.appearance().setThumbImage(UIImage(named: "sliderThumb"), for: .normal)
UISlider.appearance().setMaximumTrackImage(UIImage(named: "maximumTrack")?
	.resizableImage(withCapInsets:UIEdgeInsets(top: 0, left: 0.0, bottom: 0, right: 6.0)), for: .normal)
UISlider.appearance().setMinimumTrackImage(UIImage(named: "minimumTrack")?
	.withRenderingMode(.alwaysTemplate)
	.resizableImage(withCapInsets:UIEdgeInsets(top: 0, left: 6.0, bottom: 0, right: 0)), for: .normal)
```
##### UIProgressView
- 主要可以设置默认轨道的图片`trackImage`和进度轨迹的图片`progressImage`；

![UIProgressView](http://upload-images.jianshu.io/upload_images/1334681-45acfe6be2d0673d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
UIProgressView.appearance().trackImage = UIImage(named: "controlBackground")?
	.withRenderingMode(.alwaysTemplate)
	.resizableImage(withCapInsets: .init(top: 3, left: 3, bottom: 3, right: 3))
UIProgressView.appearance().progressImage = UIImage(named: "maximumTrack")?
	.withRenderingMode(.alwaysTemplate)
	.resizableImage(withCapInsets:UIEdgeInsets(top: 0, left: 0.0, bottom: 0, right: 6.0))
```
##### UISwitch
- 主要可以开状态的颜色`onTintColor`和拇指按钮的颜色`thumbTintColor`；
- 也可以设置开关状态的图片`onImage`和`offImage`（不过设置这两个属性后没什么效果，不建议使用）；

![UISwitch on](http://upload-images.jianshu.io/upload_images/1334681-d50a8ffad4b38e7a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
UISwitch.appearance().onTintColor = .red
UISwitch.appearance().thumbTintColor = mainColor
```
##### 其他
- 其实UIAppearance是一个协议，主要作用是返回一个`Self`类，然后通过这个代理对象设置的所有UI元素实例对象，都会保留appearance()拥有的属性值；
- 一旦设置，对所有Self类对象起作用，如果要过滤某些UI类的样式不生效，可以使用`appearance(whenContainedInInstancesOf: [])`方法；

> 一个夜间主题Demo
##### 定义一个Theme枚举

- 定义样式类型；
```
enum Theme: Int {
	case `default`, dark, graphical
	
	private enum Keys: String{
		case selected = "ThemeSelected"
	}
}
```
- 定义一个单例对象current，返回选择的样式；
```
static var current: Theme {
		return Theme.init(rawValue: UserDefaults.standard.integer(forKey: Keys.selected.rawValue)) ?? .default
	}
```
- 定义mainColor、textColor等属性；
```
var mainColor: UIColor{
		switch self {
		case .default:
			return .blue
		case .dark:
			return .orange
		case .graphical:
			return .darkGray
		}
	}
	
	var barStyle: UIBarStyle{
		switch self {
		case .default, .graphical:
			return .default
		case .dark:
			return .black
		}
	}
	
	var navigationBarBackgroundImage: UIImage?{
		return self == .graphical ? UIImage.init(named: "navBarBackground") : nil
	}
	
	var tabBarBackgroundImage: UIImage?{
		return self == .graphical ? UIImage.init(named: "tabBarBackground") : nil
	}
	
	var backgroundColor: UIColor{
		switch self {
		case .default, .graphical:
			return .white
		case .dark:
			return UIColor(white: 0.4, alpha: 1)
		}
	}
	
	var textColor: UIColor{
		switch self {
		case .default, .graphical:
			return .black
		case .dark:
			return .white
		}
	}
```
- 定义一个实例方法apply()来让选择的主题生效
```
func apply(){
	UserDefaults.standard.set(rawValue, forKey: Keys.selected.rawValue)
	UserDefaults.standard.synchronize()
	
	updateMainColor()
	
	updateNavigationBarAppearance()
	
	updateTableViewAppearance()
	
	updateLabelAppearance()
	
	updateTabBarAppearance()
	
	updateSegmentedControlAppearance()
	
	updateStepperAppearance()
	
	updateSliderAppearance()
	
	updateProgressAppearance()
	
	updateSwitchAppearance()
	
	updateActivityIndicatorAppearance()
}
```
- 设置各种UI元素的appearance（此处只举一个导航栏例子）
```
private func updateNavigationBarAppearance(){
		UINavigationBar.appearance().barStyle = barStyle
		UINavigationBar.appearance().setBackgroundImage(navigationBarBackgroundImage, for: .default)
		UINavigationBar.appearance().backIndicatorImage = UIImage(named: "backArrow")
		UINavigationBar.appearance().backIndicatorTransitionMaskImage = UIImage(named: "backArrowMaskFixed")
	}
```
##### 使用主题
- 本例中通过segmented control来切换主题
```
@IBAction func changeTheme(_ sender: UISegmentedControl) {
// 存储并设置主题
	Theme(rawValue: sender.selectedSegmentIndex)!.apply()
// TODO: 让主题立即生效
}
```

- 为了让app的window上的所有元素对主题立即生效，就务必要做到remove所有的subview，然后再addSubview，因为appearance的应用，一定是在add subview时才能起作用的
```
// TODO: 让主题立即生效
let window = UIApplication.shared.delegate?.window
window??.subviews.forEach{
	view in
	view.removeFromSuperview()
	window??.addSubview(view)
}
```
##### 自动设置夜间主题
- 这里用到了一个第三方的库[Solar](https://github.com/ceek/solar)，它是根据设置的地点的经纬度，判断应用启动时是日出还是日落，如果是日落时间段，则设置主题为dark；

```
// 北京
private let solar = Solar(latitude: 39.9047253699, longitude: 116.4072154982)!

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
	
	initializeTheme()
	
	return true
}

func initializeTheme(){
	if solar.isDaytime {
		Theme.current.apply()
		scheduleThemeTimer()
	}
	else{
		Theme.dark.apply()
	}
}
```
- 如果应用启动时是白天时间，则启动一个定时器，并加到Runloop.main队列中，一旦判断时间点为日落，则自动切换为夜间主题；
```
func scheduleThemeTimer(){
	let timer = Timer.init(fire: solar.sunset!, interval: 0, repeats: false) { [weak self] _ in
		Theme.dark.apply()
		
		self?.window?.subviews.forEach{
			view in
			view.removeFromSuperview()
			self?.window?.addSubview(view)
		}
	}
	
	RunLoop.main.add(timer, forMode: .commonModes)
}
```
##### 简书
http://www.jianshu.com/p/c63e227e40f5

> 如果对你有帮助，别忘了加个 **关注** 或 点个 **赞** 哦😁
