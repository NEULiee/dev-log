# Git

[Git Book 공식문서](https://git-scm.com/book/ko/v2)

> Git은 **분산 버전관리 시스템** (Distributed Version Control Systems - DVCS)로 컴퓨터 파일의 변경사항을 추적하고 여러명의 사용자들 간에 파일에 대한 작업을 조율하는데 사용됩니다.
> 
- Git은 데이터를 Change Set이나 변경사항(Diff)으로 기록하지 않고 일련의 `스냅샷`으로 기록합니다.

### `git add filename`

> 파일을 새로 추적할 수 있습니다 (Tracked)
> 

```markdown
$ git add README
```

### `git status`

> 파일의 상태를 확인할 수 있습니다.
> 

```markdown
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:  **-->  Staged상태 (add된 상태)**
  (use "git reset HEAD <file>..." to unstage)

    new file:   README

Changes not staged for commit:  **--> Tracked 상태 (add전 상태)**
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

### `git commit -m “commit message”`

> add로 Staged 상태가 된 파일의 변경사항을 커밋합니다.
> 

```markdown
$ git commit -m "Story 182: Fix benchmarks for speed"
[master 463dc4f] Story 182: Fix benchmarks for speed **--> master 브랜치에 커밋**
 2 files changed, 2 insertions(+)  **--> 수정된 파일 갯수, 추가된 라인 갯수**
 create mode 100644 README
```

### **`git branch 브랜치이름`**

> 새 브랜치를 생성할 수 있습니다.
> 

```markdown
$ git branch testing
```

### `git checkout 브랜치이름`

> 다른 브랜치로 이동할 수 있습니다. (브랜치로 이동하면 워킹 디렉토리의 파일이 변경됩니다.)
> 

```markdown
$ git checkout testing
```

### `**git fetch**`

> 로컬 데이터베이스에 있는 것을 뺀 리모트 저장소의 모든 것을 가져옵니다.
> 

### **`git pull`**

> git pull 명령은 git fetch와 git merge 명령을 순서대로 실행하는 것입니다. 해당 리모트에서 fetch 후 현 브랜치로 즉시 merge를 시도합니다.
> 

### **`git push`**

> git push는 리모트에는 없지만, 로컬에는 있는 커밋을 계산하여 그 차이만큼 Push 합니다.
Push를 하려면 원격 저장소에 대한 쓰기 권한이 필요하고 인증되어야 합니다.
> 

# Gist

> Git 저장 공간을 제공하는 서비스로 Code Snippet, 로그, 메모 등을 남기는데 사용합니다.
> 
- public gist : 공개적으로 누구나 접근 및 검색이 가능합니다.
- secret gist : 비공개라서 검색이 되지않고 링크를 아는 경우만 접근이 가능합니다.

## 사용방법

1. gist 생성하기 (public or private)
2. gist 저장소를 clone
3. add & commit
4. push

<br><br>

# Swift

[About Swift - The Swift Programming Language (Swift 5.7)](https://docs.swift.org/swift-book/)

[Swift 5.5: Swift Programming Language (스위프트 프로그래밍 언어)](https://xho95.github.io/swift/programming/language/grammar/2017/02/28/The-Swift-Programming-Language.html)

**Swift는 Modern Programming Pattern을 채택함으로써 일반적으로 자주 발생하는 프로그래밍 에러를 미리 방지할 수 있습니다.**

- 변수는 항상 사용하기 전에 초기화합니다.
- 배열의 인덱스는 (out-of-bounds) 범위를 벗어나는 에러를 검사합니다.
- 정수는 overflow를 검사합니다.
- 옵셔널(Optional)은 `nil` 값을 명시적으로 처리하도록 보장합니다.
- 메모리는 자동으로 관리합니다.
- 에러처리는 예상치 못한 실패로부터 controlled recovery(제어된 복구)를 허용합니다.

**Swift는 강력한 타입 추론 (type inference) 과 패턴 맞춤 (pattern matching) 기능에 현대적인 가벼운 구문을 조합하여, 복잡한 아이디어도 명확하고 간결하게 표현하도록 허용합니다.**

**Swift는 입출력이나 문자열 처리같은 기능을 위한 별도의 라이브러리를 불러올 필요가 없습니다. 전역에서 작성한 코드는 프로그램의 진입점 (entry point)로 사용하므로, `main()` 함수도 필요하지 않습니다. 또한 문장의 끝에 세미콜론을 작성할 필요도 없습니다.**

## Simple Values

상수를 만들려면 **`let`** 을, 변수를 만들려면 **`var`** 를 사용합니다.

상수 값은 컴파일 시간에 알 필요가 없지만, **반드시 값을 정확하게 한번 할당**해야 합니다.

상수나 변수는 반드시 할당하려는 값과 똑같은 타입이어야 하지만, 항상 타입을 명시적으로 작성하진 않아도 됩니다. **상수나 변수를 생성할 때 값을 제공하면 컴파일러가 그 타입을 추론하게 합니다.** 

## 배열과 딕셔너리

배열과 딕셔너리는 대괄호로 생성하며, 대괄호 안에 `**index**` 나 `**key**` 를 작성함으로써 원소에 접근합니다.

**마지막 원소 뒤에 쉼표가 있어도 됩니다.**

**원소를 추가하면 배열이 자동으로 커집니다.**

<br><br>

# Swit API 가이드라인

[스위프트 API 가이드라인](https://gist.github.com/godrm/d07ae33973bf71c5324058406dfe42dd)

- API를 만들 때는 사용할 때 기준으로 명확하고 편하게 만들어야 합니다.
- 명확한 표현이 압축한 간결성보다 더 중요합니다. (반복적으로 재사용하는 코드를 줄여야 합니다.)
- 모든 선언 부분에 주석을 적극적으로 작성한다면 문서를 작성하면서 얻는 인사이트가 설계에 깊은 영향을 줄 수 있습니다.
- Xcode 자동완성에서 볼 수 있도록 마크다운을 적극 활용합니다.
- 선언한 요소에 대해 설명하는 요약으로 문서를 작성합니다.
- 필요하다면 하나 이상의 문단이나 문장 요소를 추가합니다.

```swift
/// **[요약]**
/// Writes the textual representations of the given items into the standard
/// output.
///
/// **[부연 설명]**
/// You can pass zero or more items to the `print(_:separator:terminator:)`
/// function. The textual representation for each item is the same as that
/// obtained by calling `String(item)`. The following example prints a string,
/// a closed range of integers, and a group of floating-point values to
/// standard output:
///
///     print("One two three four five")
///     // Prints "One two three four five"
///
///     print(1...5)
///     // Prints "1...5"
///
///     print(1.0, 2.0, 3.0, 4.0, 5.0)
///     // Prints "1.0 2.0 3.0 4.0 5.0"
///
/// To print the items separated by something other than a space, pass a string
/// as `separator`.
///
///     print(1.0, 2.0, 3.0, 4.0, 5.0, separator: " ... ")
///     // Prints "1.0 ... 2.0 ... 3.0 ... 4.0 ... 5.0"
///
/// The output from each call to `print(_:separator:terminator:)` includes a
/// newline by default. To print the items without a trailing newline, pass an
/// empty string as `terminator`.
///
///     for n in 1...5 {
///         print(n, terminator: "")
///     }
///     // Prints "12345"
///
/// **[매개변수 영역]**
/// - Parameters:
///   - items: Zero or more items to print.
///   - separator: A string to print between each item. The default is a single
///     space (`" "`).
///   - terminator: The string to print after all items have been printed. The
///     default is a newline (`"\n"`).
/// **[심볼 명령]**
public func print(_ items: Any..., separator: String = " ", terminator: String = "\n")
```

## 이름짓기 Naming

- 명확한 사용법을 이름으로 제시합니다.
- 쓸모없는 단어를 제거합니다.
- 변수, 매개변수, 연관 타입은 선언한 타입이나 제약사항 보다는 **역할에 맞는 이름**을 갖도록 합니다.
- 매개변수 **역할을 명확하게 넣어서** 부족한 타입 정보를 보완합니다.

## 말하는 것처럼 술술 써지도록 작성합니다.

- 메소드나 함수를 사용할 때 영어 문장을 작성하는 것처럼 제공합니다.
- 팩토리 메소드 이름은 `make`로 시작합니다.
    - ex) `x.makeIterator()`
- 초기화(생성) 메소드나 팩토리 메소드에서 첫 번째 인자에 추가적인 설명을 포함하지 않도록 합니다.
    
    ```swift
    좋음
    let foreground = Color(red: 32, green: 64, blue: 128)
    
    나쁨
    let foreground = Color(havingRGBValuesRed: 32, green: 64, andBlue: 128)
    ```
    
- 함수나 메소드 이름은 부작용(side-effects) 여부에 따라 다르게 정합니다.
    - 부작용이 없는 경우는 명사형 ex) `x.distance(to: y)`
    - 부작용이 있는 경우는 명령형 ex) `print(x)`, `x.sort()`
    - 가변/불변 메소드 이름을 함께 고려합니다.
    - 동사로 표현하면 자연스럽게 “ed”나 “ing”를 붙여서 불변 메소드 이름을 만들 수 있습니다.
    
    > 가변 : `x.sort()`, `x.append(y)`
    > 
    
    > 불변 : `z = x.sorted()`, `z = x.appending(y)`
    > 
    - • 동작을 명사로 표현하기 적합한 경우에는 가변 메소드 이름에 "form-"을 머릿말로 붙입니다.
- 불변으로 사용할 때 Boolean 메소드나 프로퍼티를 사용할 때는 리턴 값을 받아서 단언 구문 (Assertion)처럼 읽도록 합니다.
    
    ex) `x.isEmpty`, `line1.intersects(line2)`
    
- **어떤 것을 표현하는 프로토콜은 명사처럼 읽도록 명시합니다.** ex) `Collection`
- **기능이나 가능성을 표현하는 프로토콜은 -able, -ible, -ing 등을 붙여서 표현합니다.** ex) `Equatable`, `ProgressReporting`.
- 그 외에 **상수, 변수, 속성, 타입들은 명사로 읽도록 명시합니다.**

## 용어를 잘 표현합니다

- 애매한 용어를 피합니다.
- 전문 용어를 사용한다면 기존 의미에 맞춰서 사용합니다.
- **축약어를 지양합니다.**
- 선례를 받아드려 기존 문화에 맞춰진 표현은 줄이지 않습니다. (Array, List → Array)

## 규칙

### 일반 규칙

- O(1) 복잡도가 아닌 연산 프로퍼티(Computed Property)는 설명을 만듭니다.
- 소속이 없는 자유로운 함수를 만들기 보다는 메소드나 속성을 만듭니다.
    - 예외) 명확하게 self가 없을 때 : `min(x, y)`
    - 제약없는 제네릭 함수인 경우 : `print(x)`
    - 함수 표현이 특정한 도메인 표기법을 준수하는 경우 : `sin(x)`
- 대소문자 표기법을 따릅니다.
    - 타입이나 프로토콜 이름은 `UpperCamleCase`
    - 그 외에는 모두 `LowerCamelCase`
- 메소드가 같은 의미를 갖고 있거나 특정한 도메인 영역에서만 동작을 하는 경우에는 **기본 이름을 공유할 수 있습니다.**
    - 단 “리턴 타입만 오버로딩"하는 방식은 타입 추론에 혼란을 주기 때문에 지양합니다.

### 매개 변수

- 문서화 할 수 있는 매개 변수 이름을 선택합니다.
- 매개변수 흔히 넘기는 기본값을 지정해서 편리함을 더합니다.

### 인자 레이블

```swift
func move(from: start: Point, to end: Point)
x.move(from: x, to: y)
```

- 레이블이 인자값을 구분하는데 도움이 안된다면 모든 레이블을 생략합니다.
- 초기화 생성함수에서 다른 타입 값을 받아서 변환하고 보관하는 경우에는 첫 번째 인자 레이블을 생략합니다. 
ex) `Int64(someUInt32)`
- 첫 번째 인자값이 (영어에서) 전치사 형태라면 인자값 레이블을 표기합니다. 
ex) `x.removeBoxes(havingLength: 12)`
- 첫 번째 인자값이 (전치사가 아니라) 다른 문법상의 구문이라면 레이블은 생략하고
, `x.addSubview(y)` 처럼 기본 이름에 의미있는 단어를 뒤에 붙여도 됩니다.
- 기본값이 있는 인자 값은 생략가능해서 문법상 의미있는 역할을 하지 못하기 때문에 반드시 레이블이 있어야합니다.
- 그 외에 모든 경우에는 레이블을 표기합니다.

### 특별 지침

- 튜플 멤버에 레이블을, 클로저 매개변수에 이름을 표기합니다.
- `Any` 나 `AnyObject`, 제약없는 제네릭 매개변수처럼 **제약없는 다형성(polymorphism)은 오버로드할 때 혼동하지 않도록 주의합니다.**

<br><br>

# Swift 언어의 특징

## Static Typing 정적 타이핑

> 코드를 작성할 때 컴퓨터적 구조(데이터 타입)을 명시해줍니다.
> 
- 코드의 안정성과 정교함이 커집니다.
- 코드를 실행하는 속도가 빠릅니다.
- 코드의 구조를 파악하기 쉽습니다.
- 크고 복잡하며 여러 사람들이 함께 참여하는 프로젝트에 적합합니다.

[](https://seongonion.tistory.com/16)

## Duck-type System

> 동적 타이핑의 한 종류로, 객체의 변수 및 메소드의 집합이 객체의 타입을 결정하는 것을 말합니다.
> 

클래스 상속이나 인터페이스 구현으로 타입을 구분하는 대신, 덕 타이핑은 **객체가 어떤 타입에 걸맞은 변수와 메소드를 지니면 객체를 해당 타입에 속하는 것으로 간주**합니다.

## Type Inference 타입 추론

> 선언과 동시에 초기화하여 **컴파일러가 초기화된 값을 보고 타입을 추론하는 것입니다.**
> 

```swift
let name = "Amy"
```

- 컴파일러가 초기값을 추론할 때 [Character, String] [Float, Double] 과 같이 자료형을 유추하기 애매할 때 더 큰 범위의 자료형으로 지정됩니다.

### Bi-directional

[양방향 타입추론](https://sanichdaniel.tistory.com/42)

- Bottom-up 타입추론
    
    ```swift
    let x = 0          // x is Int Type
    let name = "Amy"   // name is Type String Type  
    ```
    
- Top-Down 타입추론
    1. Literal Expression
    
    ```swift
    let y : Double = 2 // y is Double Type
    ```
    
    1. Implicit member expression
    
    ```swift
    enum Season {
        case spring
        case summer
        case fall
        case winter
    }
    
    var season = Season.summer          // season is Season Type
    season = .fall
    ```
    
    1. closures
    
    ```swift
    let numbers = [1, -2, 3]            // numbers is Array<Int> Type
    let positiveNumbers = numbers.filter { n in n >= 0 } -> numbers의 타입에 의해 추론
    print(positiveNumbers)              // [1, 3]
    ```
    
    1. Overload Resolution 함수 오버로드
    
    ```swift
    func f() -> Int {
        return 2
    }
    
    func f() -> String {
        return "test"
    }
    
    let x = f()                   // error: ambiguous use of 'f()'
    let y: Int = f()              // Overload Resolution picks f: () -> Int
    let z: String = f()           // Overload Resolution picks f: () -> String
    ```
    

### HM Type System (Hindley-Milner Type System)

- 코드의 표현식이 어떤  타입인지 수학적으로 표시할 수 있습니다.
