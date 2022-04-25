---
title: Swift 스타일 가이드
tags:
- Swift Style Guide
- Code Convention
---

개발 시 선호하는 Swift 스타일 가이드(코드 컨밴션)을 기록해 봅니다. :sunglasses:

<!--more-->

- [목적](#목적)
- [규칙](#규칙)
- [참고자료](#참고자료)

# 목적
스타일 가이드 또는 코딩 규약의 목적은 아래 순서와 같음

1. 명확함 (Clarity)
2. 일관성 (Consistency)
3. 간결함 (Brevity)


# 규칙

## 코드 레이아웃
### Xcode 설정 (Xcode Preferences)
- 라인의 Indent 값을 2 또는 4 spaces 로 통일
    + 설정 후 소스 파일에서 `Control + I` 로 Indent 값을 수정할 수 있음

 ![xcode-preferences-1](/attachments/2022-04-25/xcode-preferences-1.png){:width="700px"}

- 라인의 최대 글자수를 제한 할 수 있음
    + `Display > Page guide at column` 옵션을 활성화하고, 원하는 글자수 입력

- 코드 뒤에 불필요한 Whitespace 제거
    + `Editing > Automatically trim trailing whitespace` 옵션을 활성화

![xcode-preferences-2](/attachments/2022-04-25/xcode-preferences-2.png){:width="700px"}

    
### 코드 구조 (Code Organization)
- `// MARK - ` 구문을 이용하여 코드를 구분

```
// MARK: - Properties

// MARK: IBOutlet Properties
@IBOutlet weak var sampleView: UIView!

// MARK: Instance Properties
var sampleText: String

// MARK: - Methods

// MARK: Lifecycle Methods
override func viewDidLoad() { ... }
deinit { ... }

// MARK: Private Methods
private func samplePrivate() { ... }

// MARK: Public Methods
func samplePublic() { ... }
```

### 프로토컬 적용 (Protocol Conformance)
- 프로토컬 구현 부분은 따로 extension으로 분리

`선호`{:.success}
```
class MyViewController: UIViewController {
  // class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate methods
}
```

`비선호`{:.error}
```
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all methods
}
```

### 임포트 (Import)
- 필요한 프레임워크만 임포트
    + UIKit 임포트 시에 Foundation 은 불필요
- 내장 프레임워크를 먼저 임포트하고, 뒤에 서드파티 프레임워크 임포트
    + 구분을 위해 빈 라인 추가

`선호`{:.success}
```
import UIKit

var view: UIView
var deviceModels: [String]
```

```
import UIKit
import WebKit

import RxSwift
import RxCocoa
```

`비선호`{:.error}
```
import UIKit
import Foundation

var view: UIView
var deviceModels: [String]
```

```
import RxSwift
import UIKit
import WebKit
import RxCocoa
```

### 그 외
- 파일의 마지막에 개행 추가


## 코딩 스타일
### 중괄호 (Parentheses)
- 함수 또는 조건문의 중괄호는 같은 라인에서 시작

`선호`{:.success}
```
if user.isHappy {
  // do something
} else {
  // do something else
}
```

`비선호`{:.error}
```
if user.isHappy 
{
  // do something
} 
else 
{
  // do something else
}
```

### 콜론 (Colons)
- 왼쪽에는 공백이 없고, 오른쪽에 공백을 하나 추가
- 예외 케이스
    + 삼항 연산자 → ? : 
    + 빈 Dictionary → [:]
    + #selector 문법 → addTarget(_:action:)

`선호`{:.success}
```
class TestDatabase: Database {
  var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```

`비선호`{:.error}
```
class TestDatabase : Database {
  var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```

### 타입 추론 (Type Inference)
- 문맥 상 타입 추론이 가능한 경우 사용

`선호`{:.success}
```
let message = "Click the button"
let currentBounds = computeViewBounds()
var names = ["Mic", "Sam", "Christine"]
let maximumWidth: CGFloat = 106.5 # CGFloat 가 없으면 Double로 타입추론 됨

let selector = #selector(viewDidLoad)
view.backgroundColor = .red
let toView = context.view(forKey: .to)
let view = UIView(frame: .zero)
```

`비선호`{:.error}
```
let message: String = "Click the button"
let currentBounds: CGRect = computeViewBounds()
var names = [String]()

let selector = #selector(ViewController.viewDidLoad)
view.backgroundColor = UIColor.red
let toView = context.view(forKey: UITransitionContextViewKey.to)
let view = UIView(frame: CGRect.zero)
```

### 타입 주석 (Type Annotation)
- 빈 Array 또는 Dictionary 인 경우

`선호`{:.success}
```
var names: [String] = []
var lookup: [String: Int] = [:]
```

`비선호`{:.error}
```
var names = [String]()
var lookup = [String: Int]()
```

### 클로저 표현식 (Closure Expressions)
- 클로저가 1개인 경우 파라미터 이름은 생략
- 클로저가 여러 개인 경우 파라미터 이름을 생략하지 않음

`선호`{:.success}
```
UIView.animate(withDuration: 1.0) {
  self.myView.alpha = 0
}

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}, completion: { finished in
  self.myView.removeFromSuperview()
})
```

`비선호`{:.error}
```
UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
})

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}) { f in
  self.myView.removeFromSuperview()
}
```

- 파라미터와 리턴 타입이 없는 클로저 정의 시 () -> Void 사용

`선호`{:.success}
```
let completionBlock: (() -> Void)?
```

`비선호`{:.error}
```
let completionBlock1: (() -> ())?
let completionBlock2: ((Void) -> (Void))?
```

### 옵셔널 (Optional)
- nil 값이 허용되는 경우에 선언
-  Implicitly unwapped type(!) 은 특정 경우가 아니면 사용하지 않음
    + 반드시 초기화 될 것이 약속된 인스턴스 변수에서만 사용
- 변수 명에 optional 과 같은 접두사를 붙이지 않음
    + 옵셔널 바인딩 시에도 unwrapped 와 같은 접두사를 붙이지 않음

`선호`{:.success}
```
var subview: UIView?
var volume: Double?

if let subview = subview, let volume = volume {
  // do something with unwrapped subview and volume
}
```

`비선호`{:.error}
```
var optionalSubview: UIView?
var volume: Double!

if let unwrappedSubview = optionalSubview {
  if let realVolume = volume {
    // do something with unwrappedSubview and realVolume
  }
}
```

### Self 오브젝트 (Self Object)
- 불필요한 경우 사용하지 않음
- 클로저에서 [unowned self] 보다 [weak self] 를 사용
- self 바인딩 시에 strongSelf 와 같은 이름을 사용하지 않음
- self 바인딩이 필요없는 예외 케이스는 사용하지 않음 
    + 예시 : GCD, UIView.animate, PromiseKit 등

`선호`{:.success}
```
resource.request().onComplete { [weak self] response in
  guard let self = self else { return }

  let model = self.updateModel(response)
  self.updateUI(model)
}
```

`비선호`{:.error}
```
// might crash if self is released before response returns
resource.request().onComplete { [unowned self] response in
  let model = self.updateModel(response)
  self.updateUI(model)
}


// deallocate could happen between updating the model and updating UI
resource.request().onComplete { [weak self] response in
  let model = self?.updateModel(response)
  self?.updateUI(model)
}
```

### 코멘트 (Comments)
- 코멘트가 노출되어야 하는 경우 `\\\` 를 사용함
    + 소스 옆에 인라인으로 코멘트를 달면 노출되지 않음 주의
- C 스타일의 코멘트는 가급적이면 피함 `/* ... */`

`선호`{:.success}
```
/// Comments that require exposure
func commentMethod() {
}

/// Multiline comment
///
/// ...
```

`비선호`{:.error}
```
func commentMethod() { // not exposed
}

/*
 Multiline comment
 ...
*/
```


## 네이밍
### 클래스
- UpperCamelCase 를 사용
- 접두사(Prefix)를 붙이지 않음

### 함수
- lowerCamelCase 를 사용
- 함수 이름에 get 또는 set 접두사를 쓰지 않도록 노력
    + 명확한 의미 전달이 필요하면 붙일 수 있음

`선호`{:.success}
```
func name(for user: User) -> String?
```

`비선호`{:.error}
```
func GetName(for user: User) -> String?
```

### 상수
- lowerCamelCase 를 사용
- k 와 같은 접두사를 붙이지 않음
- enum 을 만들어 비슷한 상수끼리 모을 수 있음

`선호`{:.success}
```
let maximumNumberOfLines = 3

private enum Metric {
  static let profileImageViewLeft = 10.f
  static let profileImageViewRight = 10.f
  static let nameLabelTopBottom = 8.f
  static let bioLabelTop = 6.f
}
```

`비선호`{:.error}
```
let kMaximumNumberOfLines = 3
let MAX_LINES = 3
```

### 열거형
- 각 case 에는 lowerCamelCase 를 사용

`선호`{:.success}
```
enum Result {
  case success
  case failure
}
```

`비선호`{:.error}
```
enum Result {
  case Success
  case Failure
}
```

### Delegate
- 프로토컬 명으로 네임스페이스를 구분

`선호`{:.success}
```
protocol UserCellDelegate {
  func userCellDidSetProfileImage(_ cell: UserCell)
  func userCell(_ cell: UserCell, didTapFollowButtonWith user: User)
}
```

`비선호`{:.error}
```
protocol UserCellDelegate {
  func didSetProfileImage()
  func followPressed(user: User)

  /// `UserCell`이라는 클래스가 존재할 경우 컴파일 에러 발생
  func UserCell(_ cell: UserCell, didTapFollowButtonWith user: User)
}
```

### 약어
- 약어로 시작하는 경우 소문자로 표기하고, 그 외에는 항상 대문자로 표시

`선호`{:.success}
```
let userID: Int?
let html: String?
let websiteURL: URL?
let urlString: String?
```

`비선호`{:.error}
```
let userId: Int?
let HTML: String?
let websiteUrl: NSURL?
let URLString: String?
```

## 이름 짓기
### 동사의 변형

| **동사 원형** | **과거 분사** |
|---|---|
| request (요청하다) | requested (요청된) |
| make (만들다) | made (만들어진) |
| hide (숨다) | hidden (숨겨진) |

- 동사 원형
    + '~한다' 라는 행위의 의미로, 크게 세 군데에서 사용

```
1. 함수 및 메서드
2. Bool 변수 (조동사 + 동사원형)
 - canBecomeFirstResponder, shouldRefresh 등
3. Life Cycle 관련 delegate 메서드 (조동사 + 동사원형)
 - didFinish, willAppear, didComplete 등
```

- 과거 분사
    + 동사의 의미를 형용사로 쓰고 싶을 때 사용

```
1. 명사 수식
 - requestedData, hiddenView
2. Bool 변수
 - isHidden, isSelected
```

### 단수와 복수
- 인스턴스 하나는 단수형으로 이름 짓고, Array 타입은 복수형으로 이름 지음
- 특수한 경우가 아니면 List 나 Array를 뒤에 붙이지 않음

`선호`{:.success}
```
let album: Album
let albums: [Album]
```

`비선호`{:.error}
```
let albumList: [Album]
let albumArray: [Album]
```

### 타입별 변수명
- 일반적으로 타입을 변수명 뒤에 붙이지 않음
- 예외 경우로 Raw 한 데이터 타입인 경우 변수명에 타입을 붙여줌

```
var fullSizeImageURL: URL?     // PHContentEditingInput
var thumbnailURL: URL?         // MLMediaObject
var referenceURL: URL          // SCNReferenceNode

var referenceImage: ARReferenceImage?   // ARImageAnchor
var iconImage: NSImage?                 // MLMediaGroup

var physicalSize: CGSize               // ARReferenceImage
var startDate: Date 
var adjustmentData: PHAdjustmentData?  // PHContentEditingInput
```

### 중복 제거
- 불필요하게 의미가 중복되는 것은 제거

`선호`{:.success}
```
struct User {
  let identifier: String
}
...
let id = user.identifier

struct ImageDownloader {
  func fetch(from url: URL) { ... }
}
...
let image = imageDownloader.fetch(from: url)
```

`비선호`{:.error}
```
struct User {
  let userID: String
}
...
let id = user.userID


struct ImageDownloader {
  func downloadImage(from url: URL) { ... }
}
...
let image = imageDownloader.downloadImage(from: url)
```

### 스위프트의 Getter
- 어떤 인스턴스를 리턴하는 함수나 메서드에 get 을 쓰지 않음
- get 없이 바로 타입 이름(명사)으로 시작함

```
func date(from string: String) -> Date?
func anchor(for node: SCNNode) -> ARAnchor?                          
func distance(from location: CLLocation) -> CLLocationDistance        
func track(withTrackID trackID: CMPersistentTrackID) -> AVAssetTrack? 
```

### 데이터를 가져오는 함수 (fetch, request, perform)
- Fetch : 결과를 바로 리턴할 때
    + 동기적인 작업
    + 결과가 0인 경우를 제외하고, 실패하지 않는 종류의 작업

```
// PHAsset - Photos Framework
class func fetchAssets(withLocalIdentifiers identifiers: [String], options: PHFetchOptions?) -> PHFetchResult<PHAsset>

// PHAssetCollection - Photos Framework
class func fetchAssets(in assetCollection: PHAssetCollection, options: PHFetchOptions?) -> PHFetchResult<PHAsset>

// NSManagedObjectContext - Core Data
func fetch<T>(_ request: NSFetchRequest<T>) throws -> [T] where T : NSFetchRequestResult
```

- Request : 유저에게 요청하거나 작업이 실패할 수 있을 때
    + 비동기 작업으로 handler 또는 delegate 콜백으로 결과를 전달
    + 결과 타입이 옵셔널이고, 실패하여 Error를 전달하는 종료의 작업
    + 유저에게 특정 권한을 요청하는 메서드

```
// PHImageManager
func requestImage(for asset: PHAsset, targetSize: CGSize, contentMode: PHImageContentMode, options: PHImageRequestOptions?, resultHandler: @escaping (UIImage?, [AnyHashable : Any]?) -> Void) -> PHImageRequestID

// PHAssetResourceManager
func requestData(for resource: PHAssetResource, options: PHAssetResourceRequestOptions?, dataReceivedHandler handler: @escaping (Data) -> Void, completionHandler: @escaping (Error?) -> Void) -> PHAssetResourceDataRequestID

// CLLocationManager
func requestAlwaysAuthorization()
func requestLocation()

// MLMediaLibrary
class func requestAuthorization(_ handler: @escaping (MPMediaLibraryAuthorizationStatus) -> Void)
```

- Perform 또는 Execute : 작업의 단위가 클러져나 Request 로 래핑될 때
    + 파라미터로 클로져나 Request 객체를 받는 작업

```
// VNImageRequestHandler
func perform(_ requests: [VNRequest]) throws

// PHAssetResourceManager
func performChanges(_ changeBlock: @escaping () -> Void, completionHandler: ((Bool, Error?) -> Void)? = nil)

// NSManagedObjectContext
func perform(_ block: @escaping () -> Void)

// CNContactStore
func execute(_ saveRequest: CNSaveRequest) throws

// NSFetchRequest
func execute() throws -> [ResultType]
```

## 용어 사용
- 켜다 / 끄다
    + `선호`{:.success} turn on / turn off
    + `비선호`{:.error} activate / deactivate

- 화면에 나타남
    + `선호`{:.success} appear
    + `비선호`{:.error} display

- 버튼 액션
    + `선호`{:.success} click, tap
    + `비선호`{:.error} press (물리적 버튼)

- 체크박스 액션
    + `선호`{:.success} select / deselect
    + `비선호`{:.error} click, check / uncheck


# 참고자료
- 애플 문서 : [API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/)
- SE-0005 : [Better Translation of Objective-C APIs Into Swift](https://github.com/apple/swift-evolution/blob/master/proposals/0005-objective-c-name-translation.md)
- Raywenderlich 에서 사용하는 스타일 가이드 : [The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
- StyleShare 에서 작성한 스타일 가이드 : [StyleShare Swift Style Guide](https://github.com/StyleShare/swift-style-guide)
- 애플 문서에 사용되는 용어 정보 : [Apple Style Guide](https://help.apple.com/applestyleguide/#/)