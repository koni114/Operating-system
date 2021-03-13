# chapter04 Thread management
- thread --> 실이라는 뜻!

## 프로세스와 스레드
~~~
    (1.할당)
------------- 자원       
|               ^
|               |
v               |
프로세스 -------|
        (2.제어)
~~~
- 프로세스는 자원을 할당받아 제어 수행하면서 목적 달성
- 이때 "제어"에 할당하는 부분이 thread
- "~" -> thread를 지칭하는 기호
- <b>하나의 프로세스 안에 여러개의 thread가 있을 수 있음</b>

## 스레드(thread)
![img](https://github.com/koni114/Operating-system/blob/master/img/os_7.JPG)

### Resource
- Resource에는 코드, 전역 데이터, Heap 등이 있을 수 있음
- 코드 --> pc register 같은 녀석들이 어디 코드를 읽을 것인지 확인하여 access 할 것임
- 전역 데이터 --> 사용할 전역 Data
- Heap --> 코드를 수행할 공간

### 제어 영역
- 제어 정보는 SP, PC, 상태정보, Stack 등이 있을 수 있음
- 지역 데이터는 for문 안에서 사용되는 변수들을 의미할 수 있는데, 이는 결국 제어를 위해 사용됨
- 이러한 지역 데이터들은 stack에 저장
- <b>결과적으로 제어 영역에 해당하는 process를 우리는 thread라고 부름</b>
- <b>process 안에는 여러개의 thread이고 자원을 공유한다라는 개념을 꼭 기억하자</b>

## thread의 메모리 관점
![img](https://github.com/koni114/Operating-system/blob/master/img/os_8.JPG)

- 위의 그림은 process의 메모리 공간
- 같은 프로세스의 스레드들은 동일한 주소 공간을 공유함
- thread마다 각자의 작업영역을 가짐
- 즉 thread stack pointer들은 공유되는 자원(코드)를 제어함!

## 스레드(thread)
- Light Weight Process(LWP) 라고도 부름  
  why? process는 제어 + 자원인데, thread는 자원을 공유하고 제어만 가지고 있는 부분이기 때문
- processor 활용의 기본 단위(process가 아니고 processor!)
- 스레드 구성요소
  - thread ID
  - Resister set(pc, sp 등)
  - Stack(ex) Local data)
- 제어 요소 외에 코드, 데이터 및 자원들은 프로세스 내 다른 스레드들과 공유
- 전통적인 프로세스 = 단일 프로세스

## single thread vs multi thread
- process 내에 1개의 thread만 있으면 single thread, 여러 개의 thread가 존재하면 multi thread

## thread의 장점
- 자원공유(효율성 증가)
  - 만약 P1, P2라는 두 process가 자원 A를 공유하면 동시에 공유할 수 없으므로 context switch가 발생
  - 만약 T1, T2라는 두 thread가 자원 A를 공유하면 context switch 없이 자원 공유 가능  
    즉 커널의 개입을 막게되므로 overhead가 감소됨
- 경제성
  - process의 생성, context switch에 비해 효율적
- Multi-processor(CPU)의 활용
  - 병렬처리를 통한 성능 향상  
    processor의 활용 기본 단위임을 기억하자
- 사용자 응답성
  - multi-thread가 가능하기 때문에 스레드 처리가 지연되더라도 다른 스레드는 작업 처리 가능  
    ex) 게임을 할 때, 마우스를 움직이면서 화면 움직이면서 등등 멀티 스레드가 되지 않으면 이러한 것들이 수행될 수 없음!

## thread의 구현
- 사용자 수준 스레드(user thread)
- 커널 수준 스레드(kernel thread)

### 사용자 수준 스레드
- 사용자 영역의 스레드 라이브러리로 구현됨
  - 스레드의 생성, 스케줄링 등
  - POSIX threads, Win32 threads, Java thread API 등































