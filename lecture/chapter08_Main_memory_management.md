# 메모리 관리(Main memory management)
## 메모리(기억장치)의 종류
![img](https://github.com/koni114/Operating-system/blob/master/img/os_67.JPG)

## 메모리(기억장치) 계층구조
![img](https://github.com/koni114/Operating-system/blob/master/img/os_68.JPG)
- Block
  - 보조기억장치와 주기억장치 사이의 데이터 전송 단위
  - Size: 1 ~ 4KB
- Word
  - 주기억장치와 레지스터 사이의 데이터 전송 단위
  - Size : 16 ~ 64bits   

## Address Binding
- 프로그램의 논리 주소를 실제 메모리의 물리 주소로 매핑(mapping)하는 작업
- Binding 시점에 따른 구분
  - Compile time binding
  - Load time binding
  - Run time binding
![img](https://github.com/koni114/Operating-system/blob/master/img/os_69.JPG)

![img](https://github.com/koni114/Operating-system/blob/master/img/os_70.JPG)

## Address Binding
- Compile time binding
  - 프로세스가 메모리에 적재될 위치를 컴파일러가 알 수 있는 경우
    - 위치가 변하지 않음
  - 프로그램 전체가 메모리에 올라가야 함
- Load time binding
  - 메로리 적재 위치를 컴파일 시점에서 모르면,
    대체 가능한 상대 주소를 생성
  - 적재 시점(load time)에 시작 주소를 반영하여 사용자 코드 상의 주소를 재설정
  - 프로그램 전체가 메모리에 올라가야 함          
  
  ![img](https://github.com/koni114/Operating-system/blob/master/img/os_71.JPG)

  - Run-time binding
    - Address binging을 수행시간까지 연기
      - 프로세스가 수행 도중 다른 메모리 위치로 이동할 수 있음
    - HW의 도움이 필요
      - MMU : Memory Management Unit
    - 대부분의 OS가 사용
  
![img](https://github.com/koni114/Operating-system/blob/master/img/os_72.JPG)

## Dynamic Loading
- 모든 루틴을 교체 가능한 형태로 디스크에 저장
- 실제 호출 전까지는 루틴을 적재하지 않음
  - 메인 프로그램만 메모리에 적재하여 수행
  - 루틴의 호출 시점에 address binding 수행
- 장점
  - 메모리 공간의 효율적 사용   

## Swapping
- 프로세서 할당이 끝나고 수행 완료 된 프로세스는 swap-device로 보내고(Swap-out)
- 새롭게 시작하는 프로세스는 메모리에 적재(Swap-in)

![img](https://github.com/koni114/Operating-system/blob/master/img/os_73.JPG)

## Memory allocation
- Continuous Memory Alocation(연속할당)
  - Uni-programming
  - Multi-programming
    - Fixed partition(FPM)
    - variable partition(VPM)
- Non-continuous Memory Allocation(비연속할당) 
  - Next chapter !    