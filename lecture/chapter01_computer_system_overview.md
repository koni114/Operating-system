# chapter01 computer system overview
- cpu, gpu, memory, SSD/HDD, LAN 등 게임을 하기 위해서는 다음과 같은 것들이 필요
- 하지만 게임을 하기 위해서는 OS도 필요하다

## OS란
- HW를 효율적으로 관리해주는 SW
- 사용자, 응용프로그램에게 서비스를 제공하는 S/W

## 컴퓨터 하드웨어
- processor  
  - 계산하는 녀석
  - cpu, gpu, 응용 전용 장치
- memery
  - 저장하는 녀석
  - 주기억장치, DRAM, Disk 등
- 주변장치
  - 키보드/마우스, 모니터, 프린터

## Processor
- 컴퓨터의 두뇌(중앙처리장치)
- 연산수행
- 컴퓨터의 모든 장치의 동작 제어
~~~
# processor 구성

  레지스터  <-----
                    제어 장치
  연산장치  ---->
~~~

## 레지스터
- 프로세서 내부에 있는 메모리
- 프로세서가 저장할 데이터 저장
- 컴퓨터에서 가장 빠른 메모리

### 레지스터 종류
- 용도
  - 전용레지스터
  - 범용레지스터
- 사용자 정보 변경 가능 여부
  - 가시 레지스터
  - 불가시 레지스터
- 저장하는 정보의 종류
  - 데이터  
  - 주소  
  - 상태  
- 사용자 가시 레지스터
  - 데이터 레지스터 --> 데이터 저장
  - 주소 레지스터 --> 주소 저장
- 사용자 불가시 레지스터
  - PC(program counter) : 다음에 설명할 명령어의 주소를 보관하는 레지스터
  - 명령어 레지스터(instruction register) : 현재 실행하는 명령어를 보관하는 레지스터
  - 누산기(Accumulator) : 데이터 일시적 저장

### processor의 동작
- ALU라는 연산장치를 기반으로 다양한 레지스터들을 이용해 동작함
- OS는 프로세서를 관리하는 역할을 포함함
  - 프로세서에게 처리할 작업 할당 및 관리
  - 프로그램의 프로세서 사용 제어

## memory
- 저장하는 장치(기억장치)
- 프로그램을 저장함(ex) os, 사용자 sw, 사용자 데이터)
- 레지스터 <- 캐시 <- 메인 메모리 <- 보조기억장치
  -  왼쪽으로 갈수록 비용과 성능은 높아짐
  - 오른쪽으로 갈수록 용량이 높아짐

### memory의 종류
- 주기억장치(main memory)
  - ex) DRAM, DDR4
  - 프로세서 수행시 데이터는 main memory 안에 들어가 있어야 함   
    이유는 프로세서는 main memory까지만 접근하고 Disk는 못감
  - 역사적으로 cpu speed는 많이 증가하였으나, disk speed는 큰변화가 없음  
    따라서 둘 사이의 속도의 병목현상을 해결하기 위하여 주기억장치 등장
  - cpu가 일을 하는 동안 disk에서 memory에 미리 가져다 둠
- 캐시(cache)
  - cpu 안에 들어가 있음
  - processor 옆에 register보다 더 멀리 떨어져 있음
  - main memory와 cpu 사이의 병목현상을 해결해 주기 위하여 존재
  - L1 cache의 용량은 128kB인데 너무 작은 용량이 아닐까? 
- 캐시의 동작
  - 일반적으로 HW(cpu)가 알아서 해결해 줌
  - 프로세서가 우선적으로 캐시에 데이터가 있는지 확인  
    - 없으면 메인 메모리에 들려 캐시에 두고 가져감(--> cache miss)
    - 있으면 캐시에서 가져감(--> cache hit)
  - 만약 캐시에 데이터가 있으면 속도를 절약. 아니면 오히려 손해
  - 지역성(locality)
    - 지역성 때문에 캐시가 128kb여도 성능을 낼 수 있음
    - 공간적 지역성 : 참조한 주소와 인접한 주소를 참조하려는 특성  
      ex) 순차적 program
    - 시간적 지역성 : 한번 참조한 주소를 다시 참조하는 특성  
      ex) for문 등의 순환문
    - 지역성은 캐시 적중률(cache hit ratio)과 밀접!  
      즉 128KB로 작아도 병목현상 해결 가능
  - 보조기억장치  
     - ex) USB, CD, 등..
     - 프로세서가 직접 접근할 수 없음(주변장치)
     - 쓰고 싶으면 메모리에 데이터를 올려놓고 사용해야 함
     - 실행하려는 프로그램이 20GB인데, 메모리가 8GB인 어떻게 쓸 수 있는가?  
       - vitual memory를 통해 사용 가능
- 메모리도 운영체제가 관리하는 중요한 녀석 중 하나

## 캐시 지역성
- 1번과 2번중 어느 것이 더 빠를까?
~~~
for(i = 0; i <= n; i++){
    for(j = 0; j <= m; j++){
        x = x + a[i][j]  # -- 1
        x = x + a[j][i]  # -- 2  
    }
}
~~~
- 캐시는 데이터를 가져올 때 딱 그 부분만 가져오는 것이 아니라 block 단위로 데이터를 가져오기 때문에  
  주소 공간이 더 가까운 데이터를 근접해서 가져올수록 성능이 더 빠름 --> 1번이 더 빠름!

## 시스템 버스(system bus)
- 하드웨어들이 데이터 및 신호를 주고받는 통로
- 왜 Bus 일까? 버스는 정류장이 있는데, 각각의 장치들을 정류장으로 가지는 데이터를 나르는 수단이라고 해서 bus 라고 함
- 데이터 버스, 주소 버스, 제어 버스 등이 있음. 각 개체들을 운반하는 버스라고 생각하면 됨

## 주변장치
- 프로세서와 메모리를 제외한 하드웨어들
- 입력장치, 출력장치, 저장장치
- 장치드라이버관리
  - 주변장치 사용을 위한 인터페이스 제공  
  - 각 주변장치를 벤더들이 만들어 다양한 OS에 사용하게끔 하기 위하여 API를 만듬
    ex) driver
- 인터럽트처리
  - 키보드 입력시 입력이 들어온 것을 OS에게 알려주는 녀석이 인터럽트
- 파일 및 디스크 관리