# Wanted Lab Swift Style Guide

# 목표

이 스타일 가이드를 준수함으로써

* 보다 쉽게 읽고 익숙하지 않은 코드를 이해할 수 있도록 한다.
* 코드를 보다 쉽게 유지 관리
* 간단한 프로그래머 오류 감소
* 코딩 시 인지 부하 감소

간결함이 주된 목표가 아니라는 점에 유의한다.</br>
코드는 다른 좋은 코드 품질(가독성, 단순성, 명확성 등)이 동일하게 유지되거나 개선될 경우에만 보다 간결하게 만들어야 한다.

# Guiding Tenets

* 본 가이드에 없는 가이드라인은 아래를 따른다.
    * [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
    * [![Swift:5.2](https://img.shields.io/badge/Swift-5.2-orange)]()
* 모든 규칙을 구체화하기 위해 노력한다.
* 예외사항은 거의 두지 않아야 하고, 있더라도 정당성이 높아야한다. 
* `master` 브랜치에서 `feature` 브랜치를 만들어 가이드를 수정하고, `master` 브랜치로 PR을 보내 리뷰를 통과하면 반영시킨다.

# Table of Contents

1. [Code Layout](#code-layout)
    1. [Basic Code Layout](#basic-code-layout)
    1. [Functions](#functions)
    1. [Operators](#operators)
1. [Naming](#naming)
1. [Style](#style)
    1. [Basic Style](#basic-style)
    1. [Closures](#closures)
    1. [Properties](#properties)
    1. [Optionals](#optionals)
    1. [Comments](#comments)
1. [Patterns](#patterns)
    1. [Basic Patterns](#basic-patterns)
    1. [Objects](#objects)
    1. [Types](#types) 
1. [File Organization](#file-organization)
1. [References](#references)

# Code Layout

## Basic Code Layout

#### 한 줄은 최대 110자를 넘지 않아야한다.</br>
[![Script:Xcode](https://img.shields.io/badge/Script-Xcode-blue)](resources/xcode_settings.bash) [![SwiftLint:line_length ](https://img.shields.io/badge/SwiftLint-line__length-00B588)](https://realm.github.io/SwiftLint/line_length.html) [![SwiftFormat: wrap](https://img.shields.io/badge/SwiftFormat-wrap-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#wrap)

#### 들여쓰기에는 4개의 space를 사용한다.</br>
[![Script:Xcode](https://img.shields.io/badge/Script-Xcode-blue)](resources/xcode_settings.bash)

   <details>
   
   Tip:  일부 코드 또는 모두 선택(Command-A)한 다음 Control-I(또는 편집기 ▸ Structure ▸ Re-Indent)를 선택하여 들여쓰기를 다시 할 수 있다.   
   
   </details>

#### 줄 끝에는 공백을 제거해야한다.</br>
[![Script:Xcode](https://img.shields.io/badge/Script-Xcode-blue)](resources/xcode_settings.bash) [![SwiftLint: trailing_whitespace](https://img.shields.io/badge/SwiftLint-trailing__whitespace-007A87)](https://realm.github.io/SwiftLint/trailing_whitespace.html) [![SwiftFormat: trailingSpace](https://img.shields.io/badge/SwiftFormat-trailingSpace-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#trailingSpace)

#### MARK 구문은 유효한 형식을 따르고 위와 아래에는 공백을 추가한다.</br>
[![SwiftLint: mark](https://img.shields.io/badge/SwiftLint-mark-007A87)](https://realm.github.io/SwiftLint/mark.html)  [![SwiftFormat: blankLinesAroundMark](https://img.shields.io/badge/SwiftFormat-blankLinesAroundMark-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#blankLinesAroundMark)  [![SwiftFormat: todos](https://img.shields.io/badge/SwiftFormat-todos-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#todos) 

   <details>
   
   예를 들어 ‘// MARK: …’  또는  ‘// MARK: - …’ 형식을 사용한다. 

   좋은 예:

   ```swift
   // MARK: Layout

   override func layoutSubviews() {
    // doSomething()
   }

   // MARK: Actions

   override func menuButtonDidTap() {
    // doSomething()
   }
   ```

   </details>

#### 식별자 바로 뒤에  콜론 : 을 배치하고 그 뒤에 공백을 넣는다.</br>
[![SwiftLint: colon](https://img.shields.io/badge/SwiftLint-colon-007A87)](https://realm.github.io/SwiftLint/colon.html)

   <details>

   좋은 예:

   ```swift
   var something: Double = 0
   var dict = [KeyType: ValueType]()

   class MyClass: SuperClass {
     // ...
   }
   ```

   나쁜 예:

   ```swift
   var something : Double = 0
   var dict = [KeyType:ValueType]()
   var dict = [KeyType : ValueType]()

   class MyClass : SuperClass {
     // ...
   }
   ```
   </details>
    
#### 가독성을 위해 리턴 화살표 양쪽에 공백을 둔다.</br>
[![SwiftLint: return_arrow_whitespace](https://img.shields.io/badge/SwiftLint-return__arrow__whitespace-007A87.svg)](https://realm.github.io/SwiftLint/return_arrow_whitespace.html)

  <details>

   좋은 예:

   ```swift
   func doSomething() -> String {
     // ...
   }
   func doSomething(completion: () -> Void) {
     // ...
   }
   ```

   나쁜 예:

   ```swift
   func doSomething()->String {
     // ...
   }
   func doSomething(completion: ()->Void) {
     // ...
   }
   ```

  </details>

#### TODO와 FIXME는 Warning을 발생시켜야 한다.
주석처리 지시어를 제외한 `TODO: `, `FIXME: `의 형식을 준수하여 작성한다.</br>
단, `#warning()` 키워드 안에 작성하여 강제로 Warning을 발생시킨다.

  <details>
  
  #### 왜?
  TODO와 FIXME를 추적하고 관리하여야 하기 때문이다.
  
  좋은 예:
  
  ``` swift
  func emptyFunction() {
     #warning("TODO: 추가 로직 작성 예정입니다")
  }
   
  #warning("FIXME: 파라미터 명 교체 예정입니다")
  func doSomething(complexParameterName: String) {
     // ...
  }
  
  ```
  나쁜 예:
  
  ``` swift
  func emptyFunction() {
    // TODO: 추가 로직 작성 예정입니다
  }
    
  // 파라미터 명 교체 예정입니다
  func doSomething(complexParameterName: String) {
    // ...
  }   
  ```
  
  </details>
  
## Functions

#### 메서드 간 빈 줄이 정확히 하나 있어야한다. 

#### 메서드 및 기타(if/else/switch/while/guard-else 등) 중괄호는 항상 문장과 동일한 라인에서 열렸지만 새로운 라인에서 닫힌다.</br>
[![SwiftFormat: braces](https://img.shields.io/badge/SwiftFormat-braces-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#braces)  [![SwiftFormat: elseOnSameLine](https://img.shields.io/badge/SwiftFormat-elseOnSameLine-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#elseOnSameLine)

  <details>

  좋은 예:

  ```swift
  if user.isHappy {
   // Do something
  } else {
   // Do something else
  }
  
  guard let urlString = urlString, let url = URL(string: urlString) else {
      completion(nil, nil)
      return
  }
  ```

  나쁜 예:

  ```swift
  if user.isHappy
  {
    // Do something 
  }
  else {
   // Do something else
  }
  ```

  </details>

  _예외:   `return`, `return nil` 처럼 간단하게  `guard` 로 탈출하는 경우 한 줄로 작성한다. 단, { } 안쪽에 공백을 준다._</br>
  [![SwiftFormat: spaceInsideBraces](https://img.shields.io/badge/SwiftFormat-spaceInsideBraces-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#spaceInsideBraces)

  <details>
  
  좋은 예:

  ```swift
  guard let self = self else { return false }
  ```

  나쁜 예:

  ```swift
  guard let self = self else {return false}
    
  guard let self = self else { 
    return false
  }
  ```
  </details>

#### 메서드 내의 공백은 기능을 분리해야 하지만 섹션이 너무 많으면 종종 여러 메서드로 리팩토링해야한다.

#### 함수 정의 시 매개변수나 호출 시 인수는 같은 줄에 놓거나, 줄 당 하나만 있게한다. 여러 줄로 만든다면, 각각 새 줄에 놓고 들여쓰기를 추가한다.</br>
 [![SwiftLint: multiline_arguments](https://img.shields.io/badge/SwiftLint-multiline__arguments-00B588)](https://realm.github.io/SwiftLint/multiline_arguments.html) [![SwiftLint: multiline_parameters](https://img.shields.io/badge/SwiftLint-multiline__parameters-00B588)](https://realm.github.io/SwiftLint/multiline_parameters.html) [![SwiftFormat: wraparguments](https://img.shields.io/badge/SwiftFormat-wraparguments-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#wraparguments) [![SwiftFormat: wrap](https://img.shields.io/badge/SwiftFormat-wrap-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#wrap)  [![SwiftFormat: trailingClosures](https://img.shields.io/badge/SwiftFormat-trailingClosures-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#trailingClosures)

  <details>

  좋은 예:

  ```swift
  func reticulateSplines(
    spline: [Double], 
    adjustmentFactor: Double,
    translateConstant: Int, 
    comment: String
  ) -> Bool {
    // reticulate code goes here
  }
  
  let actionSheet = UIActionSheet(
    title: "정말 계정을 삭제하실 건가요?",
    delegate: self,
    cancelButtonTitle: "취소",
    destructiveButtonTitle: "삭제해주세요"
  )
  ```

  </details>
  
#### 함수 매개변수에 closure 가 2개 이상 존재하는 경우 내려쓰기를 한다.</br>
[![SwiftLint: multiple_closures_with_trailing_closure](https://img.shields.io/badge/SwiftLint-multiple__closures__with__trailing__closure-00B588)](https://realm.github.io/SwiftLint/multiple_closures_with_trailing_closure.html)
  
  <details>
  
  좋은 예:
   ```swift
   UIView.animate(
     withDuration: 0.25,
     animations: {
       // doSomething()
     },
     completion: { finished in
       // doSomething()
    }
   )
   ```
  </details>
  
#### single-line closure는 각 중괄호 내부에 공간이 있어야 한다.</br>
[![SwiftLint: closure_spacing](https://img.shields.io/badge/SwiftLint-closure__spacing-007A87.svg)](https://realm.github.io/SwiftLint/closure_spacing.html)

   <details>

   좋은 예:

   ```swift
   let evenSquares = numbers.filter { $0 % 2 == 0 }.map { $0 * $0 }
   ```

   나쁜 예:

   ```swift
   let evenSquares = numbers.filter {$0 % 2 == 0}.map {  $0 * $0  }
   ```

   </details>

## Operators

#### infix 연산자는 양쪽에 하나의 공간이 있어야 한다.</br>
[![SwiftLint: operator_usage_whitespace](https://img.shields.io/badge/SwiftLint-operator__usage__whitespace-007A87.svg)](https://realm.github.io/SwiftLint/operator_usage_whitespace.html)</br>
이 규칙은 범위 연산자에는 적용되지 않는다(예: `1...3`) 및 postfix 또는 접두사 연산자 (예: `guest?` , `-1`).

   <details>
   
   #### 왜?

   많은 연산자가 있는 문장을 시각적으로 그룹화하기 위해 공백의 폭을 다양하게 하기 보다는 괄호를 선호한다. 

   좋은 예:

   ```swift
   let capacity = 1 + 2
   let capacity = currentCapacity ?? 0
   let mask = (UIAccessibilityTraitButton | UIAccessibilityTraitSelected)
   let capacity = newCapacity
   let latitude = region.center.latitude - (region.span.latitudeDelta / 2.0)
   ```

   나쁜 예:

   ```swift
   let capacity = 1+2
   let capacity = currentCapacity   ?? 0
   let mask = (UIAccessibilityTraitButton|UIAccessibilityTraitSelected)
   let capacity=newCapacity
   let latitude = region.center.latitude - region.span.latitudeDelta/2.0
   ```

   </details>

   _Tip: [이 스크립트](resources/xcode_settings.bash)를 실행하여 Xcode에서 일부 설정을 활성화할 수 있다. 예: "Run Script" build phase의 일부가 되게 하면된다._

**[⬆ back to top](#table-of-contents)**

# Naming

명명은 기본적으로 [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)의 가이드를 따른다. 위 문서의 내용을 여기에 정리할 수 도 있고, 새로운 가이드라인을 추가할 수도 있다.

#### 타입과 프로토콜 이름은 PascalCase를 사용하고, 그 외에는 lowerCamelCase 를 사용한다.</br>
[![SwiftLint: type_name](https://img.shields.io/badge/SwiftLint-type__name-00B588.svg)](https://realm.github.io/SwiftLint/type_name.html) [![SwiftLint: identifier_name](https://img.shields.io/badge/SwiftLint-identifier__name-00B588.svg)](https://realm.github.io/SwiftLint/identifier_name.html)

  <details>

   좋은 예:
   ```swift
   protocol SpaceThing {
    // ...
   }

   class SpaceFleet: SpaceThing {

    enum Formation {
      // ...
    }

    class Spaceship {
      // ...
    }

    var ships: [Spaceship] = []
    static let worldName: String = "Earth"

    func addShip(_ ship: Spaceship) {
      // ...
    }
   }

   let myFleet = SpaceFleet()

   ```
   
  </details>
  
  _예외: 동일한 이름의 속성이나 메서드가 더 높은 액세스 수준을 가진 경우, `private` 속성에 밑줄 접두사를 붙일 수 있다._

  <details>

  ##### 왜?
  속성이나 메서드를 backing하는 것이 설명적인 이름을 사용하는 것 보다 더 읽기 쉬울 수 있다. 예를 들어 

   좋은 예:

   * Type erasure

   ```swift
   public final class AnyRequester<ModelType>: Requester {

    public init<T: Requester>(_ requester: T) where T.ModelType == ModelType {
      _executeRequest = requester.executeRequest
    }

    @discardableResult
    public func executeRequest(
      _ request: URLRequest,
      onSuccess: @escaping (ModelType, Bool) -> Void,
      onFailure: @escaping (Error) -> Void) -> URLSessionCancellable
    {
      return _executeRequest(request, session, parser, onSuccess, onFailure)
    }

    private let _executeRequest: (
      URLRequest,
      @escaping (ModelType, Bool) -> Void,
      @escaping (NSError) -> Void) -> URLSessionCancellable

   }
   ```

   * 더 구체적인 타입을 사용하여 덜 구체적인 타입을 backing한다.

   ```swift
   final class ExperiencesViewController: UIViewController {
    // We can't name this view since UIViewController has a view: UIView property.
    private lazy var _view = CustomView()

    loadView() {
      self.view = _view
    }
   }
   ```

  </details>

#### boolean 타입은 `isSpaceship`, `hasSpacesuit` 같은 이름을 붙인다.

이것은 그들이 다른 타입이 아닌 boolean이라는 것을 분명히 한다.

#### 약어로 시작하는 경우 소문자로 표기하고, 그 외의 경우에는 항상 대문자로 표기한다.

  <details>

   좋은 예:

   ```swift
   class URLValidator {

     func isValidURL(_ url: URL) -> Bool {
       // ...
     }

     func isProfileURL(_ url: URL, for userID: String) -> Bool {
       // ...
     }
   }

   let urlValidator = URLValidator()
   let isProfile = urlValidator.isProfileURL(urlToTest, userID: idOfUser)
   ```

   나쁜 예:

   ```swift
   class UrlValidator {

     func isValidUrl(_ URL: URL) -> Bool {
       // ...
     }

     func isProfileUrl(_ URL: URL, for userId: String) -> Bool {
       // ...
     }
   }

   let URLValidator = UrlValidator()
   let isProfile = URLValidator.isProfileUrl(URLToTest, userId: IDOfUser)
   ```

   </details>

#### 이름은 가장 일반적인 부분을 먼저 쓰고 가장 구체적인 부분은 마지막에 써야 한다.

  <details>

  "가장 일반적인"의 의미는 상황에 따라 다르지만 대략적으로 "찾는 항목에 대한 검색 범위를 좁히는 데 가장 도움이 되는" 것을 의미해야 한다. 가장 중요한 것은 일관성을 지키는 것이다. 

   좋은 예:
     
   ```swift
   let titleMarginRight: CGFloat
   let titleMarginLeft: CGFloat
   let bodyMarginRight: CGFloat
   let bodyMarginLeft: CGFloat
   ```

   나쁜 예:
     
   ```swift
   let rightTitleMargin: CGFloat
   let leftTitleMargin: CGFloat
   let bodyRightMargin: CGFloat
   let bodyLeftMargin: CGFloat
   ```

  </details>

#### 이름이 모호할 경우 이름 타입에 대한 힌트를 포함한다.

  <details>

   좋은 예:

   ```swift
   let titleText: String
   let cancelButton: UIButton
   ```

   나쁜 예:

   ```swift
   let title: String
   let cancel: UIButton
   ```

  </details>

#### 이벤트 처리 함수는 과거형으로 이름 짓는다.

주어가 명확하다면 생략할 수 있다.

  <details>

   좋은 예:

   ```swift
   class ExperiencesViewController {

     private func didTapBookButton() {
       // ...
     }

     private func modelDidChange() {
       // ...
     }
   }
   ```

   나쁜 예:

   ```swift
   class ExperiencesViewController {

     private func handleBookButtonTap() {
       // ...
     }

     private func modelChanged() {
       // ...
     }
   }
   ```

  </details>

#### Object-C 스타일의 약어 접두사를 피한다.

<details>

   ####  왜?
   이름간 충돌을 피하기 위한 방식이었는데 Swift에서 더 이상 필요하지 않다. 스위프트의 타입은 해당 타입을 포함하는 모듈에 의해 자동으로 네임스페이스가 지정되며, `NS`와 같은 클래스 접두사를 추가해서는 안 된다. 서로 다른 모듈의 두 이름이 충돌하는 경우 유형 이름과 모듈 이름을 접두사로 연결하여 모호한 정보를 해제할 수 있다. 단, 혼동 가능성이 있을 때만 모듈 이름을 지정한다. 

   좋은 예:

   ```swift
   class Account {
     // ...
   }
   ```

   나쁜 예:

   ```swift
   class AIRAccount {
     // ...
   }
   ```

   </details>

#### Delegate method를 만들 때 이름 없는 첫 번째 매개 변수가 delegate source가 되어야 한다. 

  <details>

  ##### 왜?

  좋은 예:

  ```swift
  func namePickerView(_ namePickerView: NamePickerView, didSelectName name: String)
  func namePickerViewShouldReload(_ namePickerView: NamePickerView) -> Bool
  ```

  나쁜 예:

  ```swift
  func didSelectName(namePicker: NamePickerViewController, name: String)
  func namePickerShouldReload() -> Bool
  ```
  </details>

#### 함수 이름 앞에는 되도록이면 `get`을 붙이지 않는다. 

  <details>

  좋은 예:

  ```swift
  func name(for user: User) -> String?
  ```

  나쁜 예:

  ```swift
  func getName(for user: User) -> String?
  ```
  </details>

#### 뷰(`UIView` 및 하위 타입)타입 변수의 이름을 지을 때 타입 이름을 뒤에 붙여준다.
타입 이름을 줄이지 않는다. `UICollectionViewCell`, `UITableViewCell` 의 경우는 너무 길기 때문에 `Cell`만 활용한다. 

   <details>

   ##### 왜?

   어떤 기능의 뷰인지 바로 알 수 있어서 가독성이 좋아진다. 

   좋은 예:

   ```swift
   @IBOutlet weak var titleLabel: UILabel!
   @IBOutlet weak var moreButton: UIButton!
   @IBOutlet weak var collectionView: UICollectionView!
   @IBOutlet weak var bannerCell: UITableViewCell!
   ```

   나쁜 예:

   ```swift
   @IBOutlet weak var title: UILabel!
   @IBOutlet weak var moreBtn: UIButton!
   @IBOutlet weak var collection: UICollectionView!
   @IBOutlet weak var bannerTableViewCell: UITableViewCell!
   ```

   </details>

#### 테스트 이름을 한글로 작성하는 것을 허용한다. 

   <details>

   ##### 왜?

   더 빠르게 이름을 지을수 있고, 테스트를 이해할 수 있다. 
   한글로 작성하면 올바른 테스트인지 판단하기가 더 쉽다. 

   </details>

**[⬆ back to top](#table-of-contents)**

# Style

## Basic Style

   #### 쉽게 타입이 추론될 수 있다면 타입을 포함하지 않는다.</br>
   [![SwiftLint: redundant_type_annotation](https://img.shields.io/badge/SwiftLint-redundant__type__annotation-007A87)](https://realm.github.io/SwiftLint/redundant_type_annotation.html)
  <details>

  좋은 예:

  ```swift
  let host = Host()
  let selector = #selector(viewDidLoad)
  view.backgroundColor = .red
  let toView = context.view(forKey: .to)
  let view = UIView(frame: .zero)
  ```

   나쁜 예:

   ```swift
   let host: Host = Host()
   let selector = #selector(ViewController.viewDidLoad)
   view.backgroundColor = UIColor.red
   let toView = context.view(forKey: UITransitionContextViewKey.to)
   let view = UIView(frame: CGRect.zero)
   ```
  </details>

   #### 언어에 의해 요구되거나 모호함을 피하기 위한 경우가 아니라면 `self`를 사용하지 않는다.</br>
   [![SwiftFormat: redundantSelf](https://img.shields.io/badge/SwiftFormat-redundantSelf-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#redundantSelf)

  <details>

   좋은 예:

   ```swift
   final class Listing {

     init(capacity: Int, allowsPets: Bool) {
       self.capacity = capacity
       isFamilyFriendly = !allowsPets
     }

     private let isFamilyFriendly: Bool
     private var capacity: Int

     private func increaseCapacity(by amount: Int) {
       capacity += amount
       save()
     }
   }
   ```

   나쁜 예:

   ```swift
   final class Listing {

     init(capacity: Int, allowsPets: Bool) {
       self.capacity = capacity
       self.isFamilyFriendly = !allowsPets // `self.` not required here
     }

     private let isFamilyFriendly: Bool
     private var capacity: Int

     private func increaseCapacity(by amount: Int) {
       self.capacity += amount
       self.save()
     }
   }
   ```

  </details>

#### closure 에서 `self` 를  `self` 로 바인딩한다.</br>
[![SwiftFormat: strongifiedSelf](https://img.shields.io/badge/SwiftFormat-strongifiedSelf-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#strongifiedSelf)

  <details>

   좋은 예:

   ```swift
   class MyClass {

     func request(completion: () -> Void) {
       API.request() { [weak self] response in
         guard let self = self else { return }
         // Do work
         completion()
       }
     }
   }
   ```

   나쁜 예:

   ```swift
   class MyClass {

     func request(completion: () -> Void) {
       API.request() { [weak self] response in
         guard let strongSelf = self else { return }
         // Do work
         completion()
       }
     }
   }
   ```

  </details>

#### tuple 멤버의 이름을 지정하여 더욱 명확하게 표시한다.</br>
[![SwiftLint: large_tuple](https://img.shields.io/badge/SwiftLint-large__tuple-00B588)](https://realm.github.io/SwiftLint/large_tuple.html)</br>
경험상 3개 이상의 필드가 있다면, 아마 struct를 사용해야 할 것이다.

  <details>

  좋은 예:
  
   ```swift
  func whatever() -> (x: Int, y: Int) {
    return (x: 4, y: 4)
  }

  let coord = whatever()
  coord.x
  coord.y
  ```
  
  나쁜 예:
  
   ```swift
    func whatever() -> (Int, Int) {
    return (4, 4)
  }
  let thing = whatever()
  print(thing.0)

  ```

  </details>

#### 불필요한 괄호는 생략한다.</br>
[![SwiftLint: control_statement](https://img.shields.io/badge/SwiftLint-control__statement-00B588)](https://realm.github.io/SwiftLint/control_statement.html) [![SwiftLint: unneeded_parentheses_in_closure_argument](https://img.shields.io/badge/SwiftLint-unneeded__parentheses__in__closure_argument-007A87)](https://realm.github.io/SwiftLint/unneeded_parentheses_in_closure_argument.html)  [![SwiftFormat: redundantParens](https://img.shields.io/badge/SwiftFormat-redundantParens-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#redundantParens)

  <details>

   좋은 예:

   ```swift
   if userCount > 0 { ... }
   switch someValue { ... }
   let evens = userCounts.filter { number in number % 2 == 0 }
   let squares = userCounts.map { $0 * $0 }
   ```

   나쁜 예:

   ```swift
   if (userCount > 0) { ... }
   switch (someValue) { ... }
   let evens = userCounts.filter { (number) in number % 2 == 0 }
   let squares = userCounts.map() { $0 * $0 }
   ```

  </details>

#### `NSRange` 등의 경우 `Make()` 함수 대신 생성자를 사용한다.</br>
[![SwiftLint: legacy_constructor](https://img.shields.io/badge/SwiftLint-legacy__constructor-007A87.svg)](https://realm.github.io/SwiftLint/legacy_constructor.html)

   <details>
  
   좋은 예:

   ```swift
   let range = NSRange(location: 10, length: 5)
   ```

   나쁜 예:

   ```swift
   let range = NSMakeRange(10, 5)
   ```

   </details>

#### String은 `+`를 사용하여 연산하지 않는다.

   <details>

   ##### 왜?

   컴파일 시간에 영향을 주는 주요 원인이므로 지양한다.

   좋은 예:

   ```swift
   let firstName = "김"
   let secondName = "티드"
   let wholeName = "\(firstName)\(secondName)"
   ```

   나쁜 예:

   ```swift
   let firstName = "김"
   let secondName = "티드"
   let wholeName = firstName+secondName
   ```

   </details>

## Closures

#### 매개변수와 리턴 타입이 없는 closure 정의시에는 `() -> Void`를 사용한다.</br>
[![SwiftLint: empty_parameters](https://img.shields.io/badge/SwiftLint-empty_parameters-007A87)](https://realm.github.io/SwiftLint/empty_parameters.html) [![SwiftLint: void_return](https://img.shields.io/badge/SwiftLint-void__return-007A87.svg)](https://realm.github.io/SwiftLint/void_return.html)  [![SwiftFormat: void](https://img.shields.io/badge/SwiftFormat-void-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#void)

   <details>

   ##### 왜?

   가독성이 향상된다.

   좋은 예:

   ```swift
   let completionBlock: (() -> Void)?
   ```

   나쁜 예:

   ```swift
   let completionBlock: (() -> ())?
   let completionBlock: ((Void) -> (Void))?
   ```

   </details>

#### 사용되지 않은 closure 매개변수의 이름을 밑줄(`_`)로 지정한다.</br>
[![SwiftLint: unused_closure_parameter](https://img.shields.io/badge/SwiftLint-unused__closure__parameter-007A87.svg)](https://realm.github.io/SwiftLint/unused_closure_parameter.html)

   <details>

   ##### 왜?

   어떤 매개변수가 사용되고 어떤 매개변수가 사용되지 않는지 명확히 함으로써 closure를 읽을 때 필요한 인지 오버헤드가 감소한다.

   좋은 예:

   ```swift
   someAsyncThing() { _, _, argument3 in
     print(argument3)
   }
   ```

   나쁜 예:

   ```swift
   someAsyncThing() { argument1, argument2, argument3 in
     print(argument3)
   }
   ```

   </details>

  #### closure 매개변수가 마지막 끝에 하나 있다면 가능한 한 trailing closure 구문을 사용한다.</br>
  [![SwiftFormat: trailingClosures](https://img.shields.io/badge/SwiftFormat-trailingClosures-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#trailingClosures)</br>
  둘 이상이라면 평범하게 사용한다.
  
   <details>

   좋은 예:

   ```swift
   UIView.animate(withDuration: 1.0) {
       self.myView.alpha = 0
   }

   UIView.animate(withDuration: 1.0, animations: {
    self.myView.alpha = 0
   }, completion: { finished in
    self.myView.removeFromSuperview()
   })
   ```

   나쁜 예:

   ```swift
   UIView.animate(withDuration: 1.0, animations: {
    self.myView.alpha = 0
   })

   UIView.animate(withDuration: 1.0, animations: {
    self.myView.alpha = 0
   }) { f in
    self.myView.removeFromSuperview()
   }
   ```

   </details>

## Properties

#### 연산 속성이 읽기전용이라면 get 절을 생략한다.</br>
[![SwiftLint: implicit_getter](https://img.shields.io/badge/SwiftLint-implicit__getter-00B588)](https://realm.github.io/SwiftLint/implicit_getter.html)  [![SwiftFormat: redundantGet](https://img.shields.io/badge/SwiftFormat-redundantGet-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#redundantGet)

   <details>

   좋은 예:

   ```swift
   var diameter: Double {
    return radius * 2
   }
   ```

   나쁜 예:

   ```swift
   var diameter: Double {
    get {
      return radius * 2
    }
   }
   ```

   </details>

#### `Array<T>`와 `Dictionary<T: U>` 보다는 `[T]`, `[T: U]`를 사용한다.</br>
[![SwiftLint: syntactic_sugar](https://img.shields.io/badge/SwiftLint-syntactic__sugar-007A87)](https://realm.github.io/SwiftLint/syntactic_sugar.html)  [![SwiftFormat: typeSugar](https://img.shields.io/badge/SwiftFormat-typeSugar-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#typeSugar)

   <details>

   좋은 예:

   ```swift
   var messages: [String]?
   var names: [Int: String]?
   ```

   나쁜 예:

   ```swift
   var messages: Array<String>?
   var names: Dictionary<Int, String>?
   ```

   </details>

## Optionals
> ? 는 regular optionals 을 의미한다.  
>  ! 는 implicitly unwrapped optionals (암묵적으로 포장이 풀리는 옵셔널)을 의미한다.
> 가이드에서는 ? 와 ! 로 대체하여 표현한다. 

#### 가능한 한 ? 로 선언한다. 사용전 반드시 초기화되는 경우에만  ! 로 선언한다. 

   <details>

   ##### 왜?

   ! 는  런타임시 크래시의 원인이 될 수 있다.
   * 그러나, 라이프타임이 UI 라이프사이클안에 있는 사용자 인터페이스 객체는 ! 를 사용할 수 있다. 왜냐하면 그것들은 no-nil이 보장되기 때문이다.
       * XIB 파일이나 스토리보드의 객체에 연결된  `@IBOutlet` 속성, 외부에서 주입되는 속성 등 그러한 속성을 ? 로 만드는 것은 사용자가 포장을 풀기에는 너무 많은 부담을 줄 수 있다. 
   * 또한 ! 는 단위테스트에서 허용된다. 이는 위의 UI 개체 시나리오와 유사한 이유 때문이다. 
       * 테스트 fixture의 수명은 종종 테스트의 초기화함수가 아니라 테스트의 `setUp()` 메서드에서 시작하여 각 테스트를 실행하기 전에 재설정할 수 있다.

   </details>

#### ? 나 ! 변수의 값은 가능한 한 옵셔널 바인딩으로 얻는다. 

   <details>

   ##### 왜?

   ! 는  런타임시 크래시의 원인이 될 수 있다.

   </details>

#### ? 나 ! 변수로 메서드 호출할때는 옵셔널 체이닝을 사용한다. 

   <details>

   좋은 예:

   ```swift
   textContainer?.textLabel?.setNeedsDisplay()
   ```

   </details>

#### 값을 사용할 필요가 없다면 옵셔널 바인딩을 사용하지 않고 nil을 체크한다.</br>
   [![SwiftLint: unused_optional_binding](https://img.shields.io/badge/SwiftLint-unused__optional__binding-00B588.svg)](https://realm.github.io/SwiftLint/unused_optional_binding.html)

   <details>

   ##### 왜?

   옵셔널 바인딩을 사용하는 대신 nil을 체크하면 그 실행문의 의도가 무엇인지 즉시 알 수 있다.

   좋은 예:

   ```swift
   var thing: Thing?

   if nil != thing {
     doThing()
   }
   ```

   나쁜 예:

   ```swift
   var thing: Thing?

   if let _ = thing {
     doThing()
   }
   ```

   </details>

## Comments

주석은 기본적으로 [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/) 의 가이드를 따른다. 위 문서의 내용을 여기에 정리할 수 도 있고, 새로운 가이드라인을 추가할 수도 있다.

**[⬆ back to top](#table-of-contents)**

# Patterns

## Basic Patterns

#### 강제 언랩핑 옵션을 사용하지 않고 가능하면 `init` 타임에 속성을 초기화하는 것을 선호한다.</br>
[![SwiftLint: implicitly_unwrapped_optional](https://img.shields.io/badge/SwiftLint-implicitly__unwrapped__optional-00B588.svg)](https://realm.github.io/SwiftLint/implicitly_unwrapped_optional.html)</br>
두드러진 예외는 UIViewController의 `view` 속성이다.

  <details>

   좋은 예:

   ```swift
   class MyClass: NSObject {

     init() {
       someValue = 0
       super.init()
     }

     var someValue: Int
   }
   ```

   나쁜 예:

   ```swift
   class MyClass: NSObject {

     init() {
       super.init()
       someValue = 5
     }

     var someValue: Int!
   }
   ```

  </details>

#### `init()`에서 의미 있는 작업이나 time-intensive 작업을 수행하는 것을 피한다.
데이터베이스 연결 열기, 네트워크 요청, 디스크에서 대량의 데이터 읽기 등의 작업을 수행하지 않는다. 객체를 사용할 준비가 되기 전에 이러한 작업을 수행해야 하는 경우 `start()` 메서드과 같은 것을 만든다.

#### 복잡한 속성 observers를 메소드로 추출한다.

  <details>

  ##### 왜?
  
  이는 중첩성을 감소시키고, 속성 선언으로 부터 사이드이펙트를 분리해내고,  `oldValue`와 같이 암묵적으로 전달되는 매개변수를 명시적으로 사용하게 만든다. 

   좋은 예:

   ```swift
   class TextField {
     var text: String? {
       didSet { textDidUpdate(from: oldValue) }
     }

     private func textDidUpdate(from oldValue: String?) {
       guard oldValue != text else {
         return
       }

       // Do a bunch of text-related side-effects.
     }
   }
   ```

   나쁜 예:

   ```swift
   class TextField {
     var text: String? {
       didSet {
         guard oldValue != text else {
           return
         }

         // Do a bunch of text-related side-effects.
       }
     }
   }
   ```

  </details>

#### 복잡한 callback block을 메서드로 추출한다.

  <details>
  
  ##### 왜?
  
  이것은 weak-self가 야기하는 복잡성을 막고 중첩성을 감소시킨다. 

   좋은 예:

   ```swift
   class MyClass {

     func request(completion: () -> Void) {
       API.request() { [weak self] response in
         guard let self = self else { return }
         self.doSomething(with: self.property, response: response)
         completion()
       }
     }

     func doSomething(with nonOptionalParameter: SomeClass, response: SomeResponseClass) {
       // Processing and side effects
     }
   }
   ```

   나쁜 예:

   ```swift
   class MyClass {

     func request(completion: () -> Void) {
       API.request() { [weak self] response in
         if let self = self {
           // Processing and side effects
         }
         completion()
       }
     }
   }

   ```

  </details>

#### scope 시작 부분에 `guard` 사용을 선호한다.

  <details>

  ##### 왜?
  
  모든 `guard` 문을 상단에 모아놓는 것이 비즈니스 로직과 섞일때 code block에 대해 추론하는 것이 더 쉽다.

  </details>

#### `if` 문 보다는 `guard` 문을 사용하여 중첩을 최소화한다.

   <details>

   ##### 왜?

   탈출 조건에서 `throws`나 `return` 문 등을 실행하거나 옵셔널 바인딩을 해야할 때 `guard` 문을 사용하면 중첩도를 줄여서 가독성과 유지보수성을 높일 수 있다.   

   좋은 예:

   ```swift
   func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {
    guard let context = context else {
      throw FFTError.noContext
    }
    guard let inputData = inputData else {
      throw FFTError.noInputData
    }

    // use context and input to compute the frequencies
    return frequencies
   }

   guard 
    let number1 = number1,
    let number2 = number2,
    let number3 = number3 
    else {
      fatalError("impossible")
   }
   // do something with numbers
   ```

   나쁜 예:

   ```swift
   func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {
    if let context = context {
      if let inputData = inputData {
        // use context and input to compute the frequencies

        return frequencies
      } else {
        throw FFTError.noInputData
      }
    } else {
      throw FFTError.noContext
    }
   }

   if let number1 = number1 {
    if let number2 = number2 {
      if let number3 = number3 {
        // do something with numbers
      } else {
        fatalError("impossible")
      }
    } else {
      fatalError("impossible")
    }
   } else {
    fatalError("impossible")
   }
   ```

 </details>

#### 여러 종료지점에서 정리 코드가 필요한 경우 `defer` block을 사용하는 것을 고려한다.

#### 접근 제어는 가능한 한 엄격한 수준이어야 한다.

그런 행동이 필요하지 않는 한 `open`보다는 `public`, `fileprivate`보다는 `private` 쪽을 선호한다.

#### 접근 제어 지정자가 맨 앞에 놓이게 한다.</br>
[![SwiftFormat: specifiers](https://img.shields.io/badge/SwiftFormat-specifiers-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#specifiers)

   <details>

   좋은 예:

   ```swift
   class TimeMachine {  
     private dynamic lazy var fluxCapacitor = FluxCapacitor()
   }
   ```

   나쁜 예:

   ```swift
   class TimeMachine {  
     lazy dynamic private var fluxCapacitor = FluxCapacitor()
   }
   ```

   </details>

   _예외: `static` 지정자나  `@IBAction`, `@IBOutlet`, `@discardableResult` 같은 attributes_

#### 최상위 수준 타입, 함수, 변수에 명시적으로 접근 제어를 지정한다.</br>
[![SwiftFormat: redundantExtensionACL](https://img.shields.io/badge/SwiftFormat-redundantExtensionACL-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#redundantExtensionACL)</br>
하지만, 타입 정의 내에서는 같은 수준의 접근제어를 생략한다.

   <details>

   ##### 왜?

   명시적으로 표시하게 되면 항상 신중하게 결정하게 된다. 정의 내에서 동일한 접근 제어 지정자를 재사용하는 것은 중복이며, 일반적으로 기본값이 합당하다.  

   좋은 예:

   ```swift
   puplic struct Book {}
   internal apiKey : String
   private func change(options: [Option]) {}

   public class ImageDownloader {
     var links = ImageLinks()
     private var queue = OperationQueue()
   }
   ```


   나쁜 예:

   ```swift
   struct Book {}
   apiKey : String
   func change(options: [Option]) {}

   public class ImageDownloader {
     public var links = ImageLinks()
     private var queue = OperationQueue()
   }
   ```

   </details>

#### 접근제어는 extension뿐만 아니라 method, property에도 각각 설정한다.

   <details>

   좋은 예:
   ```swift
   private extension ViewController {
       private func setupViews() {}
   }
   ```

   나쁜 예:
   ```swift
   private extension ViewController {
       func setupViews() {}
   }
   ```

   </details>

#### 가능한 한 전역 함수를 정의하지 않는다.
타입 정의안에서 메서드를 정의하는 것을 선호한다.

  <details>

  ##### 왜?
  
  이것은 가독성에 도움이 된다. 더 빨리 찾을 수 있다. 전역 함수는 특정 타입이나 인스턴스와 관련이 없을 때 가장 적절하다. 

   좋은 예:

   ```swift
   class Person {
     var bornAt: TimeInterval

     var age: Int {
       // ...
     }

     func jump() {
       // ...
     }
   }
   ```

   나쁜 예:

   ```swift
   func age(of person, bornAt timeInterval) -> Int {
     // ...
   }

   func jump(person: Person) {
     // ...
   }

   ```

  </details>

#### 상수가 `fileprivate`, `private`인 경우 파일의 최상위 레벨에 놓는 것을 선호한다.
`public` 또는 `internal`인 경우 namespacing 을 위해 `static` 속성으로 정의한다.

  <details>

   좋은 예:

   ```swift
   private let privateValue = "secret"

   public class MyClass {

    public static let publicValue = "something"

    func doSomething() {
      print(privateValue)
      print(MyClass.publicValue)
    }
   }
   ```

  </details>

#### `public` 또는 `internal` 상수 및 함수를 네임스페이스로 묶고 싶을 때는 `case` 없는 `enum`을 사용한다.</br>
[![SwiftLint: convenience_type](https://img.shields.io/badge/SwiftLint-convenience__type-00B588)](https://realm.github.io/SwiftLint/convenience_type.html)</br>
네임스페이스 없이 전역 상수와 함수를 만들지 않는다. 명료함을 위해서라면 네임스페이스를 제한없이 중첩한다.

  <details>

   ##### 왜?

   `case` 없는 `enum`은 인스턴스로 만들 수 없기 때문에 순수한 네임스페이스로 잘 맞는다. 

   좋은 예:

   ```swift
   enum Environment {

    enum Earth {
      static let gravity = 9.8
    }

    enum Moon {
      static let gravity = 1.6
    }
   }
   ```

  </details>

#### 외부 소스로 부터 매핑되는 경우가 아니라면, Swift의 자동으로 매겨지는 enum 값을 그대로 사용한다.
값을 명시적으로 할당한다면 그 이유를 설명하는 comment를 추가한다. 

  <details>

   ##### 왜?

   사용자 오류를 최소화하고 가독성을 향상시키며 코드를 더 빨리 쓰려면 Swift의 자동  `enum` 값을 사용한다. 그러나 값이 외부 소스에 매핑되거나(예: 네트워크 요청에서 제공됨) 바이너리 전역에 걸쳐 사라지지 않고 유지되는 경우,  명시적으로 값을 정의하고 이 값이 매핑되는 대상을 문서화한다. 이렇게하면 누군가가 중간에 새로운 값을 추가한다고해도 기존 것을 깨뜨리지 않게 된다.

   좋은 예:

   ```swift
   enum ErrorType: String {
     case error
     case warning
   }

   /// 이것은 logging service에서 사용된다. 명시적인 값은 바이너리 전역에 걸쳐 일관성을 보장한다. 
   // swiftlint:disable redundant_string_enum_value
   enum UserType: String {
     case owner = "owner"
     case manager = "manager"
     case member = "member"
   }

   // swiftlint:enable redundant_string_enum_value
   enum Planet: Int {
     case mercury
     case venus
     case earth
     case mars
     case jupiter
     case saturn
     case uranus
     case neptune
   }

   /// 이러한 값은 서버에서 제공하므로, 여기에 명시적으로 매칭되는 값을 설정한다.
   enum ErrorCode: Int {
     case notEnoughMemory = 0
     case invalidResource = 1
     case timeOut = 2
   }
   ```
   
   나쁜 예:

   ```swift
   enum ErrorType: String {
     case error = "error"
     case warning = "warning"
   }

   enum UserType: String {
     case owner
     case manager
     case member
   }

   enum Planet: Int {
     case mercury = 0
     case venus = 1
     case earth = 2
     case mars = 3
     case jupiter = 4
     case saturn = 5
     case uranus = 6
     case neptune = 7
   }

   enum ErrorCode: Int {
     case notEnoughMemory
     case invalidResource
     case timeOut
   }
   ```
   _예외: Codable을 준수하는 타입의 경우 내부의 enum case에서는 명시적인 값을 정의한다_

  </details>

#### 가능한 한 immutable 값을 선호한다.
새 컬렉션에 추가하는 대신 `map` 과 `compactMap` 을 사용한다. 변경 가능한 컬렉션에서 요소를 제거하는 대신 `filter`를 사용한다.

   <details>

   ##### 왜?

   mutable 변수는 복잡성을 증가시키므로 가능한 한 범위를 좁히도록 한다.

   좋은 예:

   ```swift
   let results = input.map { transform($0) }

   let results = input.compactMap { transformThatReturnsAnOptional($0) }
   ```

   나쁜 예:

   ```swift
   var results = [SomeType]()
   for element in input {
     let result = transform(element)
     results.append(result)
   }

   var results = [SomeType]()
   for element in input {
     if let result = transformThatReturnsAnOptional(element) {
       results.append(result)
     }
   }
   ```

   </details>

#### Type method는 기본적으로  `static` 으로 정의한다.
메소드를 재정의해야하는 경우에는 `class` 키워드를 사용한다.

   <details>  

   좋은 예:

   ```swift
   class Fruit {
     static func eatFruits(_ fruits: [Fruit]) { ... }
   }
   ```

   나쁜 예:

   ```swift
   class Fruit {
     class func eatFruits(_ fruits: [Fruit]) { ... }
   }
   ```

   </details>

#### 클래스는 기본적으로 `final`로 정의한다.
클래스를 재정의해야하는 경우에는 `final` 키워드를 생략한다.

   <details>

   ##### 왜?

   > 호출할 `class` 구현체를 선택하는 과정은 런타임 단계에서 수행되며, 이는 dynamic dispatch로 알려져있다.
   > 런타임 오버헤드의 일정부분은 클래스 상속을 사용하는 것과 관련이 있다.
   > `final` 키워드는 메서드나 함수의 경우 오버라이드 할 수 없게 하고, 클래스는 서브클래싱 할 수 없게 한다. 
   > 이 키워드는 런타임에서 메서드나 속성을 직접 호출할 수 있게 해줄 것이며, 약간의 성능 향상을 가져온다.
   > _스위프트 4 프로토콜지향 프로그래밍 3/e 에서 요약 인용_

   좋은 예:

   ```swift
   final class SettingsRepository {
    // ...
   }
   ```

   나쁜 예:

   ```swift
   class SettingsRepository {
    // ...
   }
   ```

   </details>

#### `switch` 문에서 `enum`값 에 대해 가급적이면 `default` 케이스를 사용하지 않는다.

   <details>

   ##### 왜?

   모든 `case`를 열거하는 것은 개발자와 검토자가 새로운 `case`가 추가될 때 모든 `switch` 문장의 정확성을 고려하도록 해준다. 

   좋은 예:

   ```swift
   switch anEnum {
   case .a:
     // Do something
   case .b, .c:
     // Do something else.
   }
   ```

   나쁜 예:

   ```swift
   switch anEnum {
   case .a:
     // Do something
   default:
     // Do something else.
   }
   ```

   </details>

#### `switch` 문에서 `case` 내 처리해야 할 코드가 있는 경우에는  `break` 사용하지 않는다.

   <details>

   ##### 왜?

   `case` 내 처리해야 할 코드가 있는 경우, `case` 내에 작성된 `break`는 컴파일러에게 일만 추가 시키고, 실행되는 의미는 없는 코드가 되어버린다.

   좋은 예:

   ```swift
   switch anEnum {
   case .a:
     // Do something
   case .b, .c:
     // Do something else.
   }
   ```

   나쁜 예:

   ```swift
   switch anEnum {
   case .a:
     // Do something
     break
   default:
     // Do something
     break
   }
   ```

   </details>


#### 언어에서 필요하지 않은 경우 `return` 키워드를 생략한다.</br>
[![SwiftLint: implicit_return](https://img.shields.io/badge/SwiftLint-implicit__return-007A87)](https://realm.github.io/SwiftLint/implicit_return.html) [![SwiftFormat: redundantReturn](https://img.shields.io/badge/SwiftFormat-redundantReturn-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#redundantReturn)

  <details>
  
  좋은 예:
  
  ```swift
  ["1", "2", "3"].compactMap { Int($0) }
  
  var size: CGSize {
    CGSize(
      width: 100.0,
      height: 100.0)
  }
  
  func makeInfoAlert(message: String) -> UIAlertController {
    UIAlertController(
      title: "ℹ️ Info",
      message: message,
      preferredStyle: .alert)
  }
  ```
  
  나쁜 예:
  
  ```swift
  ["1", "2", "3"].compactMap { return Int($0) }
  
  var size: CGSize {
    return CGSize(
      width: 100.0,
      height: 100.0)
  }
  
  func makeInfoAlert(message: String) -> UIAlertController {
    return UIAlertController(
      title: "ℹ️ Info",
      message: message,
      preferredStyle: .alert)
  }
  ```
  
  </details>
  
#### 테스트코드는 Given-When-Then 패턴을 따른다.

   <details>

   [마틴파울러의 GivenWhenThen](https://martinfowler.com/bliki/GivenWhenThen.html)
   구글링으로 여러 번역본을 찾을 수 있습니다.

   </details>

#### return 되는 값만 필요한 메소드는 Computed property(연산 프로퍼티)로 정의한다.

   <details>

   좋은 예:
   ```swift
   var isMember: Bool {
       MemberManager.shared.isMember
   }
   ```

   나쁜 예:
   ```swift
   func isMember() -> Bool {
       MemberManager.shared.isMember
   }
   ```

   </details>

## Objects

객체의 public interface를 정의할 때 따르는 가이드라인

#### 디미터 법칙을 따른다. 

   <details>

   ##### 왜?

   > Law of Demeter. 낯선자에게 말하지 말고, 오직 인접한 이웃하고만 말하라.

   디미터 법칙을 따르는 코드는 메시지 전송자가 수신자의 내부 구현에 결합되지 않는다.  
   디미터 법칙을 위반한 코드를 수정하는 일반적인 방법은 `묻지 말고 시켜라`를 따르는 것이다. 객체에게 내부 구조를 묻는 대신 직접 자신의 책임을 수행하도록 시키는 것이다. 
   이 두 스타일을 따르면 자연스럽게 자율적인 객체로 구성된 유연한 협력을 얻게 된다. 

   좋은 예:

   ```swift
   public class ReservationAgency {
     func func reserve(screening: Screening, customer: Customer, audienceCount: Int) -> Reservation  {
       let fee = screening.calculateFee(audienceCount)
       Reservation(customer, screening, fee, audienceCount);
     }
   }
   ```

   나쁜 예:

   ```swift
   public class ReservationAgency {
     func reserve(screening: Screening, customer: Customer, audienceCount: Int) -> Reservation {
       let movie: Movie = screening.movie
       var fee: Int = 0

       if movie.isDiscountable {
         let discountAmount = movie.discountAmount
         fee = (movie.fee - discountAmount) * audienceCount
       } else {
         fee = movie.fee * audienceCount
       }

       return Reservation(customer, screening, fee, audienceCount);
     }
   }
   ```

   _예외: self 속성의 컬렉션 요소에는 메시지를 전송해도 좋다._

   _예외: 디미터법칙은 하나의 점을 강제하는 규칙이 아니다_

   아래 코드는 디미터법칙을 위배하지 않는다. 객체의 내부에 대한 어떤 내용도 묻지 않는다. 

   ```swift
    [1, 10, 99, 101, 1000].filter{ $0 > 100 }.map{ $0 * 10 }.first
   ```
   객체의 내부 구조가 노출되지 않는다면 법칙을 준수한 것이다. 

   </details>

#### 객체의 상태는 숨기고 행동만 외부에 공개한다.  
속성은 `private`으로 만들어서 직접 접근하지 않고, 메서드만 사용한다. 

   <details>

   ##### 왜?

   > 묻지 말고 시켜라 (Tell, Don't Ask) 원칙. 객체의 상태에 관해 묻지 않고 원하는 것을 시킨다. 

   이렇게 하면 객체에 대해서 알아야할 정보를 최소화할 수 있다. 그리고, 자연스럽게 관련 정보를 가장 잘 알고 있는 객체에게 책임을 할당할 수 있다.  외부에서 객체의 상태를 기반으로 결정을 내리게 되면 캡슐화를 위반하게 된다.

   예외:  
   1. 묻는 것 이외에는 다른 방법이 존재하지 않는 경우도 있다.
   객체에게  묻지않고 직접 그 일을 하도록 하는 경우 응집도는 높아질 수 있지만, 본질적이지 않는 책임을 떠안게 되어 객체간 결합도가 높아질수 있다. 
   2. 물으려는 객체가 정말로 데이터인 경우도 있다. 
   3. 자료구조라면 당연히 내부를 노출해야하므로 디미터 법칙을 적용할 필요가 없다.

   속성에 직접 접근해야한다면 readonly로 만들어서 외부에서 직접 수정할 수 없게 한다. 속성값 수정이 필요하면 메서드를 통해서만 가능하게한다. 

   좋은 예:

   ```swift
   public struct Movie {
       private(set) isDiscountable: Bool
       private(set) discountAmount: Int
       private(set) fee: Int
   }
   ```

   나쁜 예:

   ```swift
   public struct Movie2 {
     var isDiscountable: Bool
     var discountAmount: Int
     var fee: Int
   }
   ```

   </details>

#### 메서드의 이름은 '어떻게'가 아니라 클라이언트가 '무엇'을 원하는지를 드러내도록 짓는다.  

   <details>

   ##### 왜?

   * '어떻게'는 내부 구현을 설명하며, 설계 시점에 내부 구현에 대해 고민할 수 밖에 없다. 결과와 목적만을 포함하도록 타입과 오퍼레이션의 이름을 부여한다. 
   * 가장 추상적인 이름을 붙인다. Tip: 매우 다른 두번 째 구현을 상상한다. 그리고, 해당 메서드에 동일한 이름을 붙인다고 상상한다. 가장 추상적인 이름을 메서드에 붙이게 될 것이다. 

   좋은 예:

   ```swift
   public class TicketSeller {
     private var ticketOffice: TicketOffice

     func sell(to audience: Audience) {
       audience.buyTicket(from:ticketOffice.ticket)
     }
   }

   public class PeriodCondition {
     func isSatisfied(_ screening: Screening) { ... }
   }
   ```

   나쁜 예:

   ```swift
   public class TicketSeller {
     private var ticketOffice: TicketOffice

     func setTicket(to audience: Audience) {
       audience.setTicket(from:ticketOffice.ticket)
     }
   }

   public class PeriodCondition {
     func isSatisfiedByPeriod(_ screening: Screening) { ... }
   }
   ```

   </details>

#### 명령과 쿼리를 분리한다. 
어떤 오퍼레이션도 명령이 동시에 쿼리가 되게 하지 않는다. 

   <details>

   ##### 왜?

   > `루틴`은 어떤 절차를 묶어 호출 가능하도록 이름을 부여한 기능모듈이다.
   > `루틴`은 `프로시저`와 `함수`로 나뉜다. 
   > `프로시저`는 사이드이펙트를 발생시킬 수 있지만 값을 반환할 수 없다.
   > `함수`는 사이드이펙트를 발생시킬 수 없지만 값을 반환할 수 없다.
   > 명령 : 쿼리 = `프로시저` : `함수` 

   * 분리로 인한 긍정적인 효과
       * 쿼리의 순서를 자유롭게 변경할 수 있다.
       * 객체지향 패러다임은 객체의 상태변화라는 사이드이펙트를 기반으로 하고 있다. 명령과 쿼리를 분리하면 객체의 사이드이펙트를 제어하기가 수월해진다. 
       * 가독성이 좋아지고, 디버깅이 쉽고, 실행 결과를 예측 가능하다.

   > 함수형 프로그래밍은 사이드이펙트가 존재하지 않는 수학적인 함수를 기반으로 한다. 그래서, 실행결과를 이해하고 예측하기가 더 쉽다. 

   </details>
  
## Types
  
#### 타입의 특성을 고려하여 `class` 와 `struct`를 신중하게 선택한다.
  
  <details>
  
  ##### 왜?
  
   `struct`는 value semantics를 가지고 있다. 정체성(identity)이 없는 것에는 `struct`를 사용한다. `[a, b, c]`를 포함하는 배열은 `[a, b, c]`를 포함하는 다른 배열과 실제로 동일하며 완전히 교환할 수 있다. 첫 번째 배열을 사용하든 두 번째 배열을 사용하든 상관없다. 왜냐하면 그것들은 정확히 같은 것을 나타내기 때문이다. 그렇기 때문에 배열은 `struct`이다.
  
  `class`는 reference semantics를 가지고 있다. 정체성(identity)이나 특정한 라이프 사이클이 있는 것에 대해 `class`를 이용한다. 두 사람 객체는 서로 다르기 때문에 사람을 `class`로 모형화 할 것이다. 두 사람이 이름과 생년월일이 같다고 해서 같은 사람이 되는 것은 아니다. 그러나 1950년 3월 3일의 날짜는 1950년 3월 3일의 다른 날짜 객체와 같기 때문에 그 사람의 생년월일은 struct가 될 것이다. 날짜 자체는 정체성이 없다.
  
  </details>


**[⬆ back to top](#table-of-contents)**

# File Organization
#### 빈 줄은 한 줄로 제한한다.</br>
[![SwiftLint: vertical_whitespace](https://img.shields.io/badge/SwiftLint-vertical__whitespace-007A87.svg)](https://realm.github.io/SwiftLint/vertical_whitespace.html)  [![SwiftFormat: blankLinesBetweenScopes](https://img.shields.io/badge/SwiftFormat-blankLinesBetweenScopes-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#blankLinesBetweenScopes)

파일을 논리 그룹으로 나누기 위해 높이가 다른 빈 줄보다는 이러한 포맷팅 가이드라인을 선호한다.

#### 파일은 새로운 줄로 끝나야 한다.</br>
[![SwiftLint: trailing_newline](https://img.shields.io/badge/SwiftLint-trailing__newline-007A87.svg)](https://realm.github.io/SwiftLint/trailing_newline.html) 

#### `extension`을 사용하여 코드를 논리적인 기능 block으로 나누어지도록 구성한다.
각 `extension`은 `// MARK: -` 주석을 달아 잘 정리해야 한다.

#### 별도의 `extension`으로 `protocol` 준수를 추가한다. 

   <details>

   ##### 왜?

   관련 메서드가 프로토콜과 함께 그룹화되어 유지되며 관련 메서드를 찾기가 더 쉽고 유지보수가 용이하다.

   좋은 예:

   ```swift
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

   나쁜 예:

   ```swift
   class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
     // all methods
   }
   ```

   </details>

#### `import` 하는 모듈은 알파벳 순으로 정렬한다.</br>
[![SwiftFormat: sortedImports](https://img.shields.io/badge/SwiftFormat-sortedImports-7B0051.svg)](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md#sortedImports)</br>
내장 모듈을 먼저 놓고, 빈 줄로 세컨드파티를 구분한다. 이후 추가 빈 줄로 서드파티를 구분할 수 있다. header comment 다음에 한 줄을 띄우고 첫 import 문을 시작한다. 이외에는 import 문 사이에 빈 줄을 추가하지 않는다.  
  
   <details>

   ##### 왜?

   standard organization 방법을 통해 파일이 어떤 모듈에 의존하는지를 보다 신속하게 알아낼 수 있다.

   좋은 예:
   ```swift
    //  Copyright © 2020 Wantedlab. All rights reserved.
    //

    import UIKit

    import SecondParty

    import SnapKit
    import React
    import Toaster
   ```
   </details>

   _예외: `@testable`은 일반적인 `import` 문 뒤에 위치하고 빈 줄로 구분해야 한다._

   <details>

   좋은 예:

   ```swift
    //  Copyright © 2020 Wantedlab. All rights reserved.
    //

    import Nimble
    import Quick

    @testable import wanted
   ```

   나쁜 예:

   ```swift
   //  Copyright © 2020 Wantedlab. All rights reserved.
   //

   import Nimble
   @testable import wanted
   import Quick
   ```

   </details>
  
#### extension 파일 이름은 MyType+Anything.swift 로 명명한다. 

   <details>

   ##### 왜?

   `+` 는 짧지만 명확하게 의미를 전달한다. 확장되는 코드를 논리적인 기능 block으로 나눌 수 있으며, 가독성과 유지보수성이 좋아진다. 찾는 항목에 대한 검색 범위를 좁히는 데 도움이 된다. 

    좋은 예:

    ```swift
    AppDelegate+Additions.swift
    UIColor+HexConversion.swift
    UIImage+Rotation.swift
    UIViewController+LogTracking.swift
    ```

   </details>

**[⬆ back to top](#table-of-contents)**

# References

[Airbnb Swift Style Guide](https://github.com/airbnb/swift)

[Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)

[The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide/blob/master/README.markdown)

[Google Swift Style Guide](https://google.github.io/swift/)

[StyleShare Swift Style Guide](https://github.com/StyleShare/swift-style-guide)

오브젝트 by 조영호   

[SwiftLint Rules](https://realm.github.io/SwiftLint/rule-directory.html)

[SwiftFormater Rules](https://github.com/nicklockwood/SwiftFormat/blob/master/Rules.md)
