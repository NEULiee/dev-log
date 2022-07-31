### Apple의 Thread Programming Guide

[About Threaded Programming](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/AboutThreads/AboutThreads.html#//apple_ref/doc/uid/10000057i-CH6-SW2)

### 해석 및 런루프, 타이머 관련 글

[[iOS - swift] Run Loops (런 루프, Thread 프로그래밍, global queue에서 Timer 동작 방법)](https://ios-development.tistory.com/515)

<br><br>

# Process Scheduling

프로세스 스케줄링은 4종류로 나눌 수 있습니다.

1. **Long-term scheduling [ Job Scheduler ]**
    
    어떤 프로그램이 실행하기 위해 시스템에 들어갈지 결정하는 스케줄링입니다.
    
    Ready Queue에 올릴 프로그램을 정합니다.
    
2. **Medium-term scheduling [ Swapper ]**
    
    메인메모리로 어떤 프로세스를 추가할지 결정하는 스케줄링
    
    멀티프로그래밍의 정도를 결정합니다.
    
3. **Short-term scheduling [ CPU Scheduler ]**
    
    실행할 프로세스를 결정하는 스케줄링
    
    Ready Queue에 있는 프로세스들 중에서 어떤 프로세스를 실행할지 정하는 스케줄링
    
4. **I/O scheduling**
    
    어떤 I/O 리퀘스트를 처리할지 결정하는 스케줄링
    

![image](https://user-images.githubusercontent.com/39167842/182015714-a5663c2d-d262-45d3-aae0-a3ac4fd23dfa.png)

## Nonpreemptive 비선점형

> 프로세스가 running 상태에 있으면 종료되거나, I/O를 기다리거나 일부 운영체제 서비스를 요청하기 위해 자체적으로 차단할 때까지 계속 실행됩니다.
> 
- 특별한 일이 없다면 끝까지 실행합니다.

### FIFO ( = FCFS )

**Non-preemption 비선점**

→ 먼저 들어온 프로세스가 먼저 실행된다.

### SPN (Shortest-Process-Next) = SJF (Shortest-Job=First)

**Non-preemption 비선점**

→ 가장 짧은 프로세스가 다음에 실행된다.

### HRRN (Highest-Response-Ratio-Next)

**Non-preemption 비선점**

→ 응답 비율이 가장 큰 프로세스를 선택합니다.

## Preemptive 선점형

> 현재 실행중인 프로세스가 운영체제에 의해 중단되고 준비 상태로 이동할 수 있습니다.
> 
- Preemptive은 새로운 프로세스가 도착할 때 수행될 수 있습니다.
- Process switch가 빈번할 수 있습니다.

### Round-Robin (Time Slicing)

**preemption 선점**

→ FCFS를 기본으로 Time Quantum을 둡니다.

### SRT (Shortest-Remaining-Time)

**preemtion 선점**

- iOS 에서의 프로세스는 실행 중인 App을 의미합니다.

<br>

---

<br>

# Thread

## Concurrency 동시성, 병행성

the ability of two or more threads to execute in interleaving (or overlapping) time periods and proceed at same time

두 개 이상의 스레드가 동시에 존재하고 (또는 겹치고) 동시에 진행되는 기능입니다.

## Parallelism 병렬성

the ability of two or more threads to execute in overlapping at same time

두 개 이상의 스레드가 동시에 겹치면서 실행되는 기능

현대의 OS 는 Prcesses와 Threads의 개념을 분리하였습니다.

## Process (Task)

The unit of resource ownership is referred to as a process or task

자원 소유권의 단위, 스레드를 제외한 모든 것

## Thread (Lightweight process)

디스패치 (스케줄링)의 단위

LightWeight Process = LWP

참고로 현대 모든 OS가 멀티 스레드를 지원하지는 않습니다.

## Main Thread

프로세스마다 모두 스레드 1개씩은 가지고 있습니다. 이를 메인 스레드라고 합니다.

<br>

---

<br>

# Multithreaded Process Model

멀티스레드 모델의 여러가지 특징을 살펴봅시다.

## Address Space

프로세스의 모든 스레드는 코드, 데이터, 힙을 공유합니다.

또한 각 스레드는 자체로 **execution stack (User / Kernel)** 을 가지고 있습니다.

그림으로 살펴봅시다. 오른쪽의 멀티 스레드를 보면 위 쪽의 execution stack은 따로 가지고 있고, 아래 쪽의 코드, 데이터, 힙은 공유한다는 것을 알 수 있습니다.

## TCB (Thread Control Block)

관리에 필요한 스레드 별 정보를 포함하는 운영체제 커널의 데이터 구조입니다.

### Shared information

- Processor info: 부모 프로세스, 시간 등
- Memory: segments, page table, and stats, etc
- I/O and file: communication ports, directories amd file desciptors, etc

### Private state information

- Processor State Information: Registers
- Scheduling and State Information: ready, running and blocked

PCB는 many KB, TCM는 a few words 용량을 가지고 있기 때문에 TCB를 lightweight 하다고 합니다.

## LWP (LightWeight Process)

기존 프로세스에서 새 스레드를 생성하는 것이 새 프로세스를 생성하는 것보다 훨씬 적은 시간이 소요됩니다.

Why?

1. 프로세스보다 스레드 종료 시간이 적습니다.
2. 프로세스 간 전환보다 동일한 프로세스 내에서 두 스레드 간 전환하는 것이 성능이 좋습니다.
3. 프로세스 생성 시간 보다 스레드 생성 시간이 적습니다.

### Single-thread / Single process

한 반복문 안에서 클라이언트의 접속을 하염없이 기다립니다.

한 클라이언트의 접속을 받고 실행중인데, 그 사이에 다른 클라이언트가 온다면 클라이언트는 하염없이 기다려야 합니다. 

### Single-thread / Multi process

멀티 프로세스를 사용하기 위해서 fork로 프로세스를 생성한다면, 수많은 요청을 처리할 때 일일이 프로세스를 생성하는 일은 매우 느립니다.

### Multi-thread / Single-process

멀티 스레드 환경이라면 클라이언트의 접속을 받을 때마다 스레드만 생성해주면 되니 빠르고, 여러 클라이언트의 요청을 계속 받을 수 있습니다.

<br><br>

# Timer

[Apple Developer Documentation](https://developer.apple.com/documentation/foundation/timer)

[Timer에 대한 고찰](https://medium.com/@jungkim/timer%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B3%A0%EC%B0%B0-b10b07bdccc3)

```swift
class Timer: NSObject
```

- 타이머는 런 루프와 함께 작동합니다.
- 런 루프는 타이머에 대한 강력한 참조를 유지하므로 런 루프에 타이머를 추가한 후에 타이머에 대한 강력한 참조를 유지할 필요가 없습니다.
- 타이머는 실시간 메커니즘이 아닙니다.
- 긴 런 루프 콜아웃 동안 또는 런 루프가 타이머를 모니터링하지 않는 모드에 있는 동안 타이머의 실행 시간이 발생하면 다음에 런 루프가 타이머를 확인할 때까지 타이머가 실행되지 않습니다.
- 따라서 타이머가 실행되는 실제 시간은 훨씬 더 늦을 수 있습니다.
