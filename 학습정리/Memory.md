# 메모리 구조

- 현재 **실행되는 앱 (프로세스) 당** 코드-데이터-힙-스택 의 **메모리 영역이 각각 따로 할당**된다.
- 컴퓨터 실행 시 OS 가 메모리를 적절히 나누어서 관리한다.

| 코드 (프로그램) | 데이터 + 힙 + 스택 |
| --- | --- |
| 명령어 / 프로그램 - 프로그램 (App)이 시작되면, 해당 프로그램이 전체 (또는 일부) 복사되어 올라가는 영역 | 프로그램이 한줄 씩 실행 되면서 실제 필요한 데이터들을 사용하는 영역 |

| 코드 (프로그램) | 데이터 | 힙 | 스택 |
| --- | --- | --- | --- |
| 명령어 / 프로그램: 앱의 모든 코드 (Text) | 전역변수, 타입(static/class) 변수 - 공통으로 공유하는 데이터 | 동적할당 : 일반적으로 긴시간동안 저장 | 함수 실행을 위한 임시적 공간 |


<aside>
💡 데이터의 종류에 따라 최대의 속도와 최적의 조건으로 사용하기 위한 효율적인 메모리 구조이다.

</aside>

<br><br>

# iOS 가상메모리

[[WWDC 2018] iOS Memory Deep Dive (1/2)](https://hucet.tistory.com/38)

[iOS Memory Deep Dive - WWDC18 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2018/416)

## Virtual Memory

> 서로 다른 RAM 시스템을 통일된 Address 시스템으로  추상화하는 기술
> 
- iOS에는 백업 저장소가 없기 때문에, 메모리 데이터를 보관하기 위해 디스크를  사용하지 않아 시스템은 물리적 RAM 크키로만 제한됩니다. → 아무튼 RAM 제약이 있다.

### Clean Dirty Pages

- Virtual Memory는 공간을 **페이지**라고 불리는 Chunk로 나눕니다.
- **페이지**는 어떤 종류의 데이터도 담을 수 있는 **16KB** Chunk 입니다.

![image](https://user-images.githubusercontent.com/39167842/182015791-4c7d8967-fc92-400d-9914-8e5957f7584b.png)

### Memory Maaped files

- 50KB 크기의 JPEG가 메모리에  매핑되면 실제로 4페이지의 메모리에  매핑되거나 제공됩니다.
- 네번째 페이지는 실제로 완전히 채워지지 않았으므로 다른 용도로 사용할 수 있습니다.

![image](https://user-images.githubusercontent.com/39167842/182015808-2565acaa-2cba-418e-8b94-1007efb43273.png)

- Clean Memory
    
    디스크에서 로드할 수 있으며 (Page out) 프레임워크, 실행 코드 및 읽기 전용 파일을 포함합니다.
    
- Dirty Memory
    
    앱, 힙 할당, 싱글톤,  글로벌 생성자 및  스택으로 채워진 메모리입니다.
    
- Compressed Memory
    
    iOS 7 부터 도입되었습니다.
    
    할당은 되었으나 접근하지않은 페이지를 압축하고 접근시 페이지 압축을 해제합니다.
    
![image](https://user-images.githubusercontent.com/39167842/182015819-25114d65-76ae-46d5-9c79-121648b954a1.png)

- 사용중인 메모리는 Dirty + Compressed memory 입니다.
- clean memory는 언제든지 복원할 수 있기 때문에 쉽게 무시할 수 있습니다.

### 일반적인 App memory profile

![image](https://user-images.githubusercontent.com/39167842/182015829-ecee0058-8a2e-425a-a36f-9cffcb2d26d1.png)

- 클린 메모리는 실제로 계산되지 않습니다.
- 모든 앱에는 설치 공간 제한이 있습니다.
- extenstion 은 메모리 제약이 많습니다.
- extenstion이 메모리 한도를 초과하면 EXC_RESOURCE_EXCEPTION 이 발생합니다.

<br><br>

# Swift - ARC

[Automatic Reference Counting - The Swift Programming Language (Swift 5.6)](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)

## 참조형식 Reference Type

`Heap` 영역에 값을 저장하기 때문에 메모리의 관리가 필요하다.

> Swift의 ARC 모델 : RC (Reference Counting)을 통해 메모리를 관리한다.
> 

ex) 클래스, 클로저

<aside>
💡 Heap 영역에 할당되는 데이터는 일반적으로 오랫동안 긴시간 동안 저장이 되어야한다.
따라서 크기가 크고, 관리할 필요가 있는 데이터가 주로 저장된다.

Heap 영역에 할당되는 데이터는 관리를 해야하지만, 메모리에서 해제될 수 있다.
만약 사용하지 않는 데이터가 해제되지 않으면 **메모리 누수 (Memory Leak)** 현상이 발생한다.

</aside>

## 여러 언어의 메모리 관리

| Java | Objective - C | Swift |
| --- | --- | --- |
| GC (Garbage Collector)
런타임에 메모리를 감시하는 기법 | MRC (Manual RC) - 수동 RC 관리
ARC (Automatic RC) | ARC (Automatic RC) |
- RC (Reference Count) 으로 메모리 관리
- **컴파일 시 메모리 해제 시점을 결정**한다.

## MRC (Manual RC)

- 코드

```swift
class Point {
	var x, y: Double
	func draw() {...}
}

let point1 = Point(x: 0, y: 0)
let point2 = point1
point2.x = 5

// use point1
// use point2
```

- 컴파일된 코드

```jsx
class Point {
	**var refCount: Int            // RC**
	var x, y: Double
	func draw() {...}
}

**let point1 = Point(x: 0, y: 0) // + 1**
let point2 = point1
**retain(point2)                 // + 1**
point2.x = 5

// use point1
**release(point1)                // - 1**
// use point2
**release(point2)                // - 1**
```

<aside>
💡 예전 언어에서는 메모리를 수동으로 관리하였기 때문에 실수할 가능성도 높았다.

`retain()`  할당  -  `release()` 해제

따라서 현대적인 언어는 대부분 자동 메모리 관리 모델을 사용하게 되었다.

Swift 의 경우 컴파일러가 `retain()`, `release()` 코드를 자동으로 삽입하여 메모리 관리에 대한 안정성이 증가하게 된다.

</aside>

## ARC (Automatic Reference Counting)

### 소유정책

> 인스턴스는 **하나이상의 소유자가 있는 경우 메모리에 유지된다.**
> 

### 참조카운팅

> 인스턴스를 가르키는 **소유자 수를 카운팅한다.**
> 

<br><br>

# XCode 에서 메모리 디버깅하기

[iOS 메모리 뜯어보기, 메모리 이슈 디버깅하기, 메모리 릭 찾기](https://seizze.github.io/2019/12/20/iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0.html)

### Memory Graph Debugger

> 디버깅  창에 Memory 선택시 그래프로 메모리 용량을 볼 수 있다!  

![image](https://user-images.githubusercontent.com/39167842/182015849-74dcbf68-70d9-4476-8b13-bceb81d77b6b.png)



### Memory snapshot의 Memory 정보를 보여주는 Graph Debugger

> 왼쪽 패널에서 현재 메모리에 적재되어 있는 객체들과 해당 클래스의 인스턴스 숫자들, 각 인스턴스들의 주소 목록을 보여준다.
> 

사실 무슨의미인지는  잘 모르겠다..ㅎ
![image](https://user-images.githubusercontent.com/39167842/182015859-36dff79b-1373-4ec5-bfa4-3cc353eb6767.png)



### Command Line Tool

1. Memory Graph 파일 추출

![image](https://user-images.githubusercontent.com/39167842/182015872-6bf2aac3-26bf-40dc-8cd9-550bc5d4589d.png)


2. 터미널에서 `vmmap —summary [파일이름].memgraph` 입력
- 뭐가 주르르륵 뜬다. 현재 프로세스에 할당된 가상 메모리 공간 !!

```swift
가상 메모리 공간 사이즈, Dirty인 영역 등을 나누어 출력해 줍니다. 
여기서 Swapped Size는 iOS에서는 Compressed Size를 의미하며, 
주의할 점은 Memory compressor에 의해 압축되기 전의 사이즈를 의미한다는 것입니다.

--summary 플래그 없이 vmmap 명령어를 사용하면 
프로그램의 텍스트와 실행 코드 영역, 힙 영역 등 모든 가상 메모리 영역의 컨텐츠를 보여줍니다.

다음으로 leaks는 힙의 객체들을 추적하여 retain cycle등을 잡아내며, 
heap은 힙 영역의 객체들을 보여줍니다. 
기본적으로는 개수가 많은 순서로 출력하며, 
--sortBySize 플래그를 이용하면 크기가 큰 순서로 출력합니다.

Xcode의 Scheme editor에서 Malloc Stack Logging에 체크하면, 메모리가 할당될 때마다 기록합니다.
이 Malloc Stack Logging이 Enable되어 있을 경우, malloc_history 명령어를 사용하여 
특정 인스턴스가 언제 어떤 메서드에 의해 할당되었는지 backtrace를 알 수 있습니다.

출처: 상위 블로그
```
