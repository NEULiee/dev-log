# Crawling

[](https://www.cloudflare.com/ko-kr/learning/bots/what-is-a-web-crawler/)

> 웹 사이트에 있는 데이터를 추출해서 사용하기 위한 목적으로 홈페이지 내용을 수집하고 추출하는 것
> 
- robots.txt의 disallow 정보를 확인해서 크롤링한다.
- 콘텐츠 사용에 대한 확인 (라이센스, 페이지 약관, 사이트 문의, 법적인 확인절차 등)
- 크롤링 주기
- 외부 모듈의 사용 (Swiftsoup..)

## SwiftSoup

[https://github.com/scinfu/SwiftSoup](https://github.com/scinfu/SwiftSoup)

> macOS, iOS, tvOS, watchOS, Linux에서 지원하는 Swift 라이브러리 입니다.
> 
- URL, file 또는 문자열에서 HTML을 스크랩하여 parsing 합니다.
- DOM을 순회하거나 CSS selector를 사용하여 데이터를 추출합니다.

# Cache

> **성능개선에서 가장 많이 사용되는 방법** (클라이언트의 http 요청, 백엔드의 DB 요청 등)
> 
- 캐시의 접근 시간에 비해 원래 데이터를 접그ㅜㄴ하는 시간이 오래 걸리는 경우나 값을 다시 계산하는 시간을 절약하고 싶은 경우에 사용합니다.
- 캐시에 데이터를 미리 복사해 놓으면 계산이나 접근 시간 없이 더 빠른 속도로 데이터에 접근할 수 있습니다.

[캐시 - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EC%BA%90%EC%8B%9C)

## 캐시 교체 정책

### FIFO (First-In-First-Out)

> 가장 먼저 들어간 캐시를 교체합니다.
> 

### LFU (Least Frequently Used)

> 사용 횟수가 가장 적은 캐시를 교체합니다.
> 

### LRU (Least Recently Used) - 효율적인 캐시 교체 방식

> 가장 오랫동안 사용되지 않은 캐시를 교체합니다.
> 
- 구현방식
    - Hashmap과 Doubly LinkedList 방식으로 구현합니다.

## NSCache

[Apple Developer Documentation](https://developer.apple.com/documentation/foundation/nscache)

> 리소스가 부족하다면 (Cache 공간이 부족하다면) 자동으로 삭제되는 key-value 쌍을 임시고 저장하는 mutable collection (변경 가능한 컬렉션) 입니다.
> 

### NSCache와 Dictionary의 차이점

- NSCache는 시스템 메모리를 과도하게 사용하지 않도록하는 자동 삭제 정책을 가집니다.
    - 다른 애플리케이션에서 메모리를 필요로 할 경우 이 정책으로 인해 cache에서 일부 항목을 제거합니다.
- Thread-safe하게 구현되어 있어 따로 lock하지 않아도 다른 스레드에서 캐시의 항목 추가, 제거, 검색할 수 있습니다.
- NSDictionary 객체와 다르게 저장된 Key 객체를 복사하지 않습니다.

**NSDictionary**

- NSDictionary의 Key는 객체를 복사해서 새로운 객체를 생성하고 이를 Key로 등록합니다.

```swift
let mutableDic = NSMutableDictionary()
var dicKey: NSMutableString = "key" // K₁
mutableDic.setObject("one", forKey: dicKey) // K₂
dicKey.setString("changedKey") // still K₁
mutableDic.setObject("two", forKey: dicKey) // K₃

print(mutableDic.object(forKey: "key") ?? "") // "one"
print(mutableDic.object(forKey: "changedKey") ?? "") // "two"
```

**NSCache**

- NSCache는 객체를 복사하지않습니다.

```swift
let cache = NSCache<NSString, NSString>()
var cacheKey: NSMutableString = "key" // K₁
cache.setObject("one", forKey: cacheKey) // still K₁
cacheKey.setString("changedKey") // still K₁
cache.setObject("two", forKey: cacheKey) // still K₁!

print(cache.object(forKey: "key") ?? "") // "" 
print(cache.object(forKey: "changedKey") ?? "") // "two"
```

[[Swift] NSCache와 NSDictionary의 차이점](https://inuplace.tistory.com/1050)
