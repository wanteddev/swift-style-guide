# [Grouping Extension](https://github.com/wanteddev/swift-style-guide#extension%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EC%BD%94%EB%93%9C%EB%A5%BC-%EB%85%BC%EB%A6%AC%EC%A0%81%EC%9D%B8-%EA%B8%B0%EB%8A%A5-block%EC%9C%BC%EB%A1%9C-%EB%82%98%EB%88%84%EC%96%B4%EC%A7%80%EB%8F%84%EB%A1%9D-%EA%B5%AC%EC%84%B1%ED%95%9C%EB%8B%A4)

## Class
Class는 Class Block, IBAction Block, Public Property Block, Public Method Block, Private Property Block, Private Block, Protocol Block 순으로 구분합니다.

### Class Block
* Class Block에는 초기화가 필요한 Property와 override function, 그리고 생명주기 관련된 항목을 합니다.  
```

// MARK: - Class Block

final class ViewController: UIViewController {
    @IBOutlet weak var nameLabel: UILabel!
    private let refreshControl = UIRefreshControl()
    private var somthingHelper: SomthingHelperProtocol?

    override func viewDidLoad() {
        super.viewDidLoad()
        // ...
    }
}

```
### IBAction Block
```

// MARK: - IBAction

extension ViewController {
    @IBAction func btnDidTap(_ sender: Any?) {
        // ...
    }
}

```
### Public Property Block
```

// MARK: - Public Property

extension ViewController {
    public var isLogin: String { 
        // ...
    }
}

```
### Public Method Block
```

// MARK: - Public Method

extension ViewController {
    public func publicMethod() {
        // ...
    }
}

```
### Private Property Block
```

// MARK: - Private Property

extension ViewController {
    private var token: String { 
        // ...
    }
}

```
### Private Method Block
```

// MARK: - Private Method

extension ViewController {
    private func privateMethod() {
        // ...
    }
}

```
### Protocol Block
```

// MARK: - SomthingHelperProtocol

extension ViewController: SomthingHelperProtocol {
    func test() {
        // ...
    }
}

```
## Struct
Struct도 마찬가지로 Struct Block, Public Property Block, Public Method Block, Private Property Block, Private Block 순으로 구분합니다.
### Struct Block
* 초기화가 필요한 Property와 Initialization을 작성합니다.
```

// MARK: - Struct Block

struct User {
    let id: Int
    let firstName: String
    let lastName: String
    let company: String?
    
    init(id: Int, firstName: String, lastName: String) {
        self.id = id
        self.firstName = firstName
        self.lastName = lastName
        self.company = nil
    }
}

```
### Public Property Block
```

// MARK: - Public Property

extension User {
    var fullName: String {
        return firstName + lastName
    }
}

```
### Public Method
```

// MARK: - Public Method

extension User {
    public func hasCompany() -> Bool {
        return nil != company
    }
}

```
### Private Method
```

// MARK: - Private Method

extension User {
    private func friend() {
        // ...
    }
}

```
## Enum
Enum도 마찬가지로 Enum Block, Public Property Block, Public Method Block, Private Property Block, Private Block 순으로 구분합니다.
### Enum Block
* Enum Block은 case만 작성합니다.
```

// MARK: - Enum Block

enum Region {
    case kr
    case jp
    case sg
    case hk
    case tw
}

```
### Public Property Block
```

// MARK: - Public Property

extension Region {
    var description: String {
        switch self {
        case .kr:
            return "KR"
        case .jp:
            return "JP"
        case .sg:
            return "SG"
        case .hk:
            return "HK"
        case .tw:
            return "TW"
        }
    }
}

```
### Public Method Block
```

// MARK: - Public Method

extension Region {
    func flagImage() {
        // ...
    }
}

```
### Private Property Block
```

// MARK: - Private Property

extension Region {
    private var description: String {
        switch self {
        case .kr:
            return "KR"
        case .jp:
            return "JP"
        case .sg:
            return "SG"
        case .hk:
            return "HK"
        case .tw:
            return "TW"
        }
    }
}

```
### Private Method Block
```

// MARK: - Private Method

extension Region {
    func imageName() {
        // ...
    }
}

```


## 참고자료
- https://gwangyonglee.tistory.com/38
- https://www.natashatherobot.com/using-swift-extensions/
- https://cocoacasts.com/four-clever-uses-of-swift-extensions
- https://realm.github.io/SwiftLint/override_in_extension.html
