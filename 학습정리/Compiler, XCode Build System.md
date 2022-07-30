[컴파일러 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC)

# 컴파일러

> 특정 프로그래밍 언어로 쓰여 있는 문서를 다른 프로그래밍 언어로 옮기는 언어 번역 프로그램
> 
- 고급 프로그래밍 언어를 실행 프로그램으로 만들기 위해 저급 프로그래밍 언어 (어셈블리, object코드, machine code)로 바꾸는데 사용됩니다.
- 소스코드에서 목적코드로 옮기는 과정을 **컴파일**이라고 합니다.
    - 컴파일(빌드) 과정 : ( 전처리 → 컴파일 → 어셈블리 → 링킹 )
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


💡 Tokenizer, Lexer의 역할을 합하여 Lexical analyze라고 합니다.  
**Lexical analyze** : 의미있는 조각을 검출하여 토큰을 생성하는 것



## Parser

> Lexical analyze 으로 토큰화된 데이터를 가지고 구조적으로 나타낼 수 있게 해줍니다.
> 
- 컴파일러가 추상 구문 트리 (AST)를 생성합니다.

## 추상 구문 트리 (AST)

> Abstract Syntax Tree의 약자로 프로그래밍 언어로 쓰여진 소스코드의 추상화된 구조를 표현하기 위해 사용되는 자료구조 입니다.
> 
- 소스코드를 각각 의미별로 분리하여 컴퓨터가 이해할 수 있는 구조로 변경시킨 트리입니다.

<br><br>

# XCode Build System

[Understanding Xcode Build System](https://www.vadimbulavin.com/xcode-build-system/)

- iOS의 Language processing system을 XCode Build System이라고 합니다.
- Language processing system 언어 처리 시스템은 고급언어를 하드웨어가 이해할 수 있는 저급 언어로 변형 시키는 시스템을 의미합니다.
- XCode Build System을 포함한 대부분의 Language processing system은 5개의 파트로 구성됩니다.
    - Preprocessor
    - Compiler
    - Assembler
    - Linker
    - Loader

![image](https://user-images.githubusercontent.com/39167842/181877257-0b6416b0-39b2-4bb7-a3aa-bbbbb4d05dff.png)

## 1. Preprocessing

> preprocessing 과정의 목적은 소스 프로그램을 컴파일러에게 제공할 수 있는 방식으로 변환하는 것입니다.
> 
- It replaces macros with their definitions, discovers dependencies and resolves preprocessor directives.
(해석이 잘 안되는데.. 매크로를 정의로 대체하고, dependency를 발견하며, preprocessor 지시문을 해결합니다?)
- XCode는 하위 레벨 빌드 시스템 (lower-level build system)인 `llbuild` 를 통해 dependency를 해결합니다.

## 2. Compiler

> Compiler는 한 언어의 프로그램을 다른 언어의 의미상 동등한 프로그램으로 매핑하는 프로그램입니다.
> 
- 예를 들어 Swift, Objective-C, C/C++ 코드를 의미를 잃지 않고 동등한 기계어로 변환합니다.
- XCode는 두가지의 컴파일러를 사용합니다.
    - Swift를 위한 컴파일러
    - Objective-C를 위한 컴파일러 (Objective-C++ 및 C/C++ 파일)
- `clang`은 C언어를 위한 Apple의 공식 컴파일러 입니다. swift-clang
- `swiftc`는 XCode에서 Swift 소스코드를 컴파일하고 실행할 수 있는 Swift 컴파일러입니다.
    
    [Understanding Xcode Build System](https://www.vadimbulavin.com/xcode-build-system/)
    

- 컴파일러의 다이어그램입니다.
    
    ![image](https://user-images.githubusercontent.com/39167842/181877265-f62c9410-5966-4686-8ccf-70e7c7d32992.png)
    

- 컴파일러의 변환 과정
    
    **[Front-end]**
    
    1. 문법 구조로 프로그램을 별도의 조각으로 나눕니다.
    2. 컴파일러는 이 구조를 가지고 소스 프로그램의 `intermediate representation` 을 생성합니다.
    3. 또한 소스 프로그램에 대한 symbol table을 생성하고 관리합니다.
        
        (symbol table : 코드나 데이터 조각의 이름)
        
    4. Swift 컴파일러의 경우 `intermediate representation`을 `**Swift Intermediate Language (SIL)**` 이라고 합니다. (코드를 분석하거나 최적화하는데 사용됩니다.)
    5. `SIL`에서 바로 기계어를 생성할 수는 없습니다. 
    `SIL`은 `LLVM Intermediate Representation`으로 한번 더 변형을 거쳐야 합니다.
    
    **[Back-end]**
    
    1. `Intermediate Representation`이 `assembly code`로 변환됩니다.

## 3. Assembler

> Assembler는 사람이 읽을 수 있는 어셈블리 코드를 재배치 가능한 기계어로 변환합니다. 
그리고 코드와 데이터 모음인 Mach-O 파일을 생성합니다.
> 
- 기계어는 CPU에서 즉시 실행 가능한 명령어 모음을 나타내는 numeric 언어 입니다.
    - object 파일이 주소 공간에 어느 위치에 있든 명령은 해당 공간에 상대적으로 실행되기 때문에 재배치 가능합니다. (재배치가 왜 필요한지 모르겠습니다..)
- Mach-O 파일은 라이브러리들의 실행가능한 object 파일들에 사용되는 iOS와 macOS 운영체제의 특별한 파일입니다.
    - ARM 프로세스나 Intel 프로세서에서 실행되는 의미있는 조각들로 그룹화된 byte stream 입니다.

## 4. Linker

> Linker는 iOS나 macOS에서 실행될 수 있는 하나의 Mach-O 파일을 생성하기 위해 다양한 object 파일들과 라이브러리들을 합치는 컴퓨터 프로그램입니다. ( `.dylib`, `.tbd`, `.a` )
> 

## 5. Loader

> 마지막으로 Loader는 프로그램을 메모리로 가져와서 실행합니다.
> 
- Loader는 프로그램을 실행하는데 필요한 메모리 공간을 할당하고 레지스터를 초기 상태로 초기화합니다.

<br><br>

# iOS의 인터페이스 빌더 - 스토리보드, nib (xib)

[iOS Graphic Interface 살펴보기 (1/2)](http://labs.brandi.co.kr/2018/07/16/leejh.html)

[[swift] ios 앱 프로그래밍의 기본 - 스토리보드 파일의 이해](https://m.blog.naver.com/codnjs9999/220583427668)


💡 Storyboard와 Xib은 기본적으로 **XML 기반의 파일** 입니다.


- 혹시라도 충돌이 발생하면 UI로 확인이 불가능하기 때문에, Xcode에서 해당 Storyboard, Xib 파일을 우클릭해서 Open As > Source Code 메뉴를 클릭하면 XML 형식으로 브라우징할 수 있습니다.

## Storyboard

> Segue와 같은 시퀀스 설정을 할 수 있고, 연결된 하나의 Flow를 시각적으로 펼치기 좋은 프로토타이핑을 위한 적절한 툴
> 
- 기본 스토리보드의 xml 코드

```xml
<?xml version="1.0" encoding="UTF-8"?>
<document type="com.apple.InterfaceBuilder3.CocoaTouch.Storyboard.XIB" version="3.0" toolsVersion="13122.16" targetRuntime="iOS.CocoaTouch" propertyAccessControl="none" useAutolayout="YES" useTraitCollections="YES" useSafeAreas="YES" colorMatched="YES" initialViewController="BYZ-38-t0r">
    <dependencies>
        <plugIn identifier="com.apple.InterfaceBuilder.IBCocoaTouchPlugin" version="13104.12"/>
        <capability name="Safe area layout guides" minToolsVersion="9.0"/>
        <capability name="documents saved in the Xcode 8 format" minToolsVersion="8.0"/>
    </dependencies>
    <scenes>
        <!--View Controller-->
        <scene sceneID="tne-QT-ifu">
            <objects>
                <viewController id="BYZ-38-t0r" customClass="ViewController" customModuleProvider="target" sceneMemberID="viewController">
                    <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                        <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                        <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                        <color key="backgroundColor" xcode11CocoaTouchSystemColor="systemBackgroundColor" cocoaTouchSystemColor="whiteColor"/>
                        <viewLayoutGuide key="safeArea" id="6Tk-OE-BBY"/>
                    </view>
                </viewController>
                <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
            </objects>
        </scene>
    </scenes>
</document>
```

## Nib (Xib)

> 조각조각 단위의 화면이나 재사용을 많이하는 CollectionViewCell 등의 화면 작업에 적합합니다.
CollectionViewCell, ReusableView, Custom Component
> 
- UITableViewCell의 xml 코드

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<document type="com.apple.InterfaceBuilder3.CocoaTouch.XIB" version="3.0" toolsVersion="13142" targetRuntime="iOS.CocoaTouch" propertyAccessControl="none" useAutolayout="YES" useTraitCollections="YES" useSafeAreas="YES" colorMatched="YES">
    <dependencies>
        <plugIn identifier="com.apple.InterfaceBuilder.IBCocoaTouchPlugin" version="12042"/>
        <capability name="Safe area layout guides" minToolsVersion="9.0"/>
        <capability name="documents saved in the Xcode 8 format" minToolsVersion="8.0"/>
    </dependencies>
    <objects>
        <placeholder placeholderIdentifier="IBFilesOwner" id="-1" userLabel="File's Owner"/>
        <placeholder placeholderIdentifier="IBFirstResponder" id="-2" customClass="UIResponder"/>
        <tableViewCell contentMode="scaleToFill" selectionStyle="default" indentationWidth="10" id="KGk-i7-Jjw" customClass="XibPracticeTableViewCell" customModuleProvider="target">
            <rect key="frame" x="0.0" y="0.0" width="320" height="44"/>
            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
            <tableViewCellContentView key="contentView" opaque="NO" clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="center" tableViewCell="KGk-i7-Jjw" id="H2p-sc-9uM">
                <rect key="frame" x="0.0" y="0.0" width="320" height="43"/>
                <autoresizingMask key="autoresizingMask"/>
            </tableViewCellContentView>
            <viewLayoutGuide key="safeArea" id="njF-e1-oar"/>
        </tableViewCell>
    </objects>
</document>
```

- 이 XML 코드를 파싱하여 속성값들을 코드로 넘겨주는 과정으로 클래스 코드에 이 값들이 알맞게 대입됩니다.
- 실제 앱 빌드를 위한 모든 정보는 최종적으로 프로그램 코드에 들어가게 됩니다.
- 스토리보드 정보는 컴파일 전처리 과정 이후에는 필요없게 됩니다.
- 스토리보드는 오로지 초기 속성만을 부여할 수 있습니다.
