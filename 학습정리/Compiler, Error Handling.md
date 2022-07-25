[컴파일러 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC)

# 컴파일러

> 특정 프로그래밍 언어로 쓰여 있는 문서를 다른 프로그래밍 언어로 옮기는 언어 번역 프로그램
> 
- 고급 프로그래밍 언어를 실행 프로그램으로 만들기 위해 저급 프로그래밍 언어 (어셈블리, object코드, machine code)로 바꾸는데 사용됩니다.
- 소스코드, 원시코드 → 목적코드
- 소스코드에서 목적코드로 옮기는 과정을 **컴파일**이라고 합니다.
- 컴파일러는 소스 프로그램을 읽어서 즉시 결과를 출력하는 인터프리와는 구분됩니다. 그러나 현대에 들어 많은 인터프리터가 실시간 컴파일을 수행하므로, 컴파일러와 인터프리터 사이의 기술적 구분은 사라져 가는 추세입니다.

[컴파일러 이론에서 토크나이저(Tokenizer), 렉서(Lexer), 파서(Parse) 의 역할](https://velog.io/@mu1616/%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC-%EC%9D%B4%EB%A1%A0%EC%97%90%EC%84%9C-%ED%86%A0%ED%81%AC%EB%82%98%EC%9D%B4%EC%A0%80Tokenizer-%EB%A0%89%EC%84%9CLexer-%ED%8C%8C%EC%84%9CParse-%EC%9D%98-%EC%97%AD%ED%95%A0)

[[컴파일러] 토크나이저, 렉서, 파서 (Tokenizer, Lexer, Parser)](https://gobae.tistory.com/94)

# 컴파일러: 구문분석

## Tokenizer

> 어떤 구문에서 의미있는 요소들을 토큰으로 쪼갭니다.
> 
- 컴파일러가 소스코드 파일을 읽어서 개별 문법 요소 단위로 자릅니다.

## Lexer

> 토큰의 의미를 분석합니다.
> 

<aside>
💡 Tokenizer, Lexer의 역할을 합하여 Lexical analyze라고 합니다.
**Lexical analyze** : 의미있는 조각을 검출하여 토큰을 생성하는 것

</aside>

## Parser

> Lexical analyze 으로 토큰화된 데이터를 가지고 구조적으로 나타낼 수 있게 해줍니다.
> 
- 컴파일러가 추상 구문 트리 (AST)를 생성합니다.

## 추상 구문 트리 (AST)

> Abstract Syntax Tree의 약자로 프로그래밍 언어로 쓰여진 소스코드의 추상화된 구조를 표현하기 위해 사용되는 자료구조 입니다.
> 
- 소스코드를 각각 의미별로 분리하여 컴퓨터가 이해할 수 있는 구조로 변경시킨 트리입니다.

# 예외처리

## try

> 모든 에러발생의 예외적인 경우를 디테일하게 처리 가능
> 

```swift
do {
    let isChecked = try checkingHeight(height: 200)
    
    if isChecked {
        print("청룡열차 가능")
    } else {
        print("후룸라이드 가능")
    }
} catch {
    print("놀이기구 타는 것 불가능")
}
```

## try?

> 옵셔널 타입으로 리턴
> 
- 에러가 발생하지 않는 경우 → 리턴 타입으로 반환
- 에러가 발생하는 경우 → `nil`

```swift
let isChecked = try? checkingHeight(height: 200)      // Bool?
```

## try!

> 에러가 발생할 가능성이 없는 경우
> 
- 에러가 발생하지 않는 경우 → 리턴 타입으로 반환
- 에러가 발생하는 경우 → 에러

```swift
let isChecked2: Bool = try! checkingHeight(height: 150)      // Bool
```

## Catch

```swift
do {
    let isChecked = try checkingHeight(height: 100)
    print("놀이기구 타는 것 가능: \(isChecked)")
    
} catch HeightError.maxHeight  {    // where절을 추가해서, 
																		// 매칭시킬 에러패턴에 조건을 추가할 수 있다
    print("키가 커서 놀이기구 타는 것 불가능")
    
} catch HeightError.minHeight {      // 생략가능
    
    print("키가 작아서 놀이기구 타는 것 불가능")
    
}
```

```swift
// catch 패턴이 없이 처리도 가능

do {
    
    let isChecked = try checkingHeight(height: 100)
    print("놀이기구 타는 것 가능: \(isChecked)")
    
} catch {    // error 상수를 제공 (모든 에러가 넘어옴)
    print(error.localizedDescription)
    
    if let error = error as? HeightError {    // 실제 정의한 구체적인 에러 타입이 아니고, 
        switch error {                        // 에러 타입(프로토콜)이 넘어올 뿐
        case .maxHeight:
            print("키가 커서 놀이기구 타는 것 불가능")
        case .minHeight:
            print("키가 작아서 놀이기구 타는 것 불가능")
        }
    }
}
```

```swift
// 스위프트 5.3 버전 업데이트

do {
    
    let isChecked = try checkingHeight(height: 100)
    print("놀이기구 타는 것 가능: \(isChecked)")
    
} catch HeightError.maxHeight, HeightError.minHeight {   // 케이스 나열도 가능해짐
    
    print("놀이기구 타는 것 불가능")
    
}
```
