# chapter07 교착상태(Deadlock Resoltion)
- 어느 프로세스도 어느 자원을 가져갈 수 없는 상태

## Deadlock의 개념
- Blocked/Asleep state
  - 프로세스가 특정 이벤트를 기다리는 상태
  - 프로세스가 필요한 자원을 기다리는 상태
- Deadlock state
  - 프로세스가 발생 가능성이 없는 이벤트를 기다리는 경우
    - 프로세스가 deadlock 상태에 있음
  - 시스템 내에 deadlock에 빠진 프로세스가 있는 경우
    - 시스템이 deadlock 상태에 있음
- Deadlock vs Starvation  

![img](https://github.com/koni114/Operating-system/blob/master/img/os_48.JPG)
- deadlock은 asleep 상태에 있는데, event가 발생할 일이 없는 경우
- starvation은 ready state에서 cpu를 기다리고 있는 상태! 발생할 수는 있는데 운이 없어서 발생 안하고 있는 상태
- 즉 기다리고 있는 자원도 차이가 있음

## 자원의 분류
- 일반적 분류
  - Hardware resources vs Software resources
- 다른 분류법
  - 선점 가능 여부에 따른 분류
  - 할당 단위에 따른 분류
  - 동시 사용 가능 여부에 따른 분류
  - 재사용 가능 여부에 따른 분류  

### 선점 가능 여부에 따른 분류
- Preemptible resources
  - 선점 당한 후, 돌아와도 문제가 발생하지 않는 자원
  - Processor, memory 등
- Non-preemptible resources
  - 선점 당하면, 이후 진행에 문제가 발생하는 자원
    - Rollback, restart등 특별한 동작이 필요
  - E.g., disk drive 등  
    무엇을 작성하고 있을 때 usb를 뽑아버리면? --> non-preemptible     

### 할당 단위에 따른 분류
- Total allocation resources
  - 자원 전체를 프로세스에게 할당
  - E.g., Processor(1 core 일 때) 
  - disk drive(한번에 한 명만 사용 가능)
- Partitioned allocation resources
  - 하나의 자원을 여러 조각으로 나누어, 여러 프로세스들에게 할당
  - ex) Memory등

### 동시 사용 가능 여부에 따른 분류
- Exclisive allocation resources
  - 한 순간에 한 프로세스만 사용 가능한 자원
  - ex) processor, memory, disk drive 등
  - memory는 조각내서 사용할 순 있지만, 동일한 조각을 여러 프로세스가 공유할 수 없음
- Shared allocation resource
  - 여러 프로세스가 동시에 사용 가능한 자원 
  - ex) Program(sw), shared data 등  
    워드 프로그램 창을 여러개 띄어놓고 사용할 수 있는 것!, exe 파일 등

### 재사용 가능 여부에 따른 분류
- SR(Serially-reusable Resources)
  - 시스템 내에 항상 존재 하는 자원
  - 사용이 끝나면, 다른 프로세스가 사용 가능
  - ex) Processor, memory, disk drive, program 등 
- CR(consumable Resources)
  - 한 프로세스가 사용한 후에 사라지는 자원
  - ex) signal, message 등 

## Deadlock과 자원의 종류
- Deadlock을 발생시킬 수 있는 자원의 형태
  - Non-preemptible resources  
    한 번 사용하면 끝까지 사용하게 되므로 deadlock 가능성이 있음  
    자원을 빼앗을 수 있으면 문제는 발생 안 할 것임
  - Exclusive allocation resources  
    혼자 자원을 쓰는 경우에 deadlock 발생 가능
  - Serially reusable resources
  - 할당 단위는 영향을 미치지 않음
- CR(consumable Resources)을 대상으로 하는 Deadlock model
  - deadlock이 발생할 수 있지만, 너무 복잡하여 이번 시간에는 제외하기로 하자

## Deadlock 발생의 예
![img](https://github.com/koni114/Operating-system/blob/master/img/os_49.JPG)

- 3번 상태는 deadlock 상태는 아님. 만약 P2가 R1을 반납한다면 정상적인 프로세스 수행 가능
- 4번 상태에서는 P2가 P1이 가지고 있는 자원을 요청함으로써 절대 일어날 수 없는 event 상태가 됐으므로, deadlock 상태가 됨

## Deadlock Model(표현법)
- Graph Model
- State transition Model

### Graph Model
- Node
  - 프로세스 노드(P1, P2), 자원 노드(R1, R2)
- Edge
  - Rj -> Pi : 자원 Rj 이 프로세스 Pi에 할당 됨
  - Pi -> Rj : 프로세스 Pi가 자원 Rj을 요청(대기 중)  

![img](https://github.com/koni114/Operating-system/blob/master/img/os_50.JPG)
- 앞에 했던 deadlock 예제를 그림으로 표현한 것임
- cycle이 상태를 deadlock임을 확인할 수 있음

### State Transition Model
- 예제
  - 2개의 프로세스와 A type의 자원 2개(unit) 존재(Ra 2개)
  - 프로세스는 한번에 자원 하나만 요청/반납 가능
- State는 총 5가지 경우의 수를 가짐
![img](https://github.com/koni114/Operating-system/blob/master/img/os_51.JPG)
- 만약 프로세스가 2개라면 5x5 --> 25가지의 state를 가질 수 있음
![img](https://github.com/koni114/Operating-system/blob/master/img/os_52.JPG)
- 상태가 변하는 것을 edge로 표현
- deadlock이 S33에서 발견됨. 둘 다 하나를 잡고 하나를 요청하게 되면 deadlock임을 알 수 있음

## Deadlock 발생 필요 조건
- 아래 4가지 case를 모두 성립해야 deadlock이라는 얘기!
- 자원의 특성
  - Exclusive use of resources -- 1
  - Non-preemptible resources -- 2 
- 프로세스의 특성
  - Hold and wait(Partial allocation) -- 3 
    - 자원을 하나 hold하고 다른 자원 요청 
  - Circular wait -- 4

## Deadlock 해결 방법
- Deadlock prevention methods 
- Deadlock avoidance method
- Deadlock detection and deadlock recovery methods

## Deadlock Prevention
- 4개의 deadlock 발생 필요 조건 중 하나를 제거
  - Exclusive use of resources
  - Non-preemptible resources
  - Hold and wait(Partial allocation)
  - Circular wait
- Deadlock이 절대 발생하지 않음  
- 모든 자원을 공유 허용
  - Exclusive use of resources 조건 제거
  - 현실적으로 불가능
- 모든 자원에 대해 선점 허용
  - Non-preemptible resources 조건 제거
  - 현실적으로 불가능
  - 유사한 방법
    - 프로세스가 할당 받을 수 없는 자원을 요청한 경우, 기존에 가지고 있던 자원을 모두 반납하고 작업 취소
      - 이후 처음(또는 check-point)부터 다시 시작
    - 심각한 자원 낭비 발생 --> 비현실적      
- 필요 자원 한번에 모두 할당(Total allocation)
  - Hold and wait 조건 제거
  - 자원 낭비 발생
    - 필요하지 않는 순간에도 가지고 있음
  - 무한 대기 현상 발생 가능
- Circular wait 조건 제거
  - Totally allocation을 일반화한 방법
  - 자원들에게 순서를 부여
  - 프로세스는 순서의 증가 방향으로만 자원 요청 가능  
    한 방향으로만 요청하므로 원을 만들어 낼 수 없음 
  - 자원 낭비 발생. 내가 쓸 수 있는 자원이 있는데도 할당 못받음
- 4개의 deadlock 발생 필요 조건 중 하나를 제거
- Deadlock이 절대 발생하지 않지만 심각한 자원 낭비가 발생
- 비현실적임!