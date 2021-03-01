# Operating Systems

-------



### **1. 스케줄링**

> CPU 를 잘 사용하기 위해 프로세스를 잘 배정하기

- 조건 : 오버헤드 ↓ / 사용률 ↑ / 기아 현상 ↓
- 목표
  1. `Batch System`: 가능하면 많은 일을 수행. 시간(time) 보단 처리량(throughout)이 중요
  2. `Interactive System`: 빠른 응답 시간. 적은 대기 시간.
  3. `Real-time System`: 기한(deadline) 맞추기.

### **2. 선점 / 비선점 스케줄링**

- 선점 (preemptive) : OS가 CPU의 사용권을 선점할 수 있는 경우, 강제 회수하는 경우
- 비선점 (nonpreemptive) : 프로세스 종료 or I/O 등의 이벤트가 있을 때까지 실행 보장 (처리시간 예측 어려움)

### **3. 프로세스 상태**

![https://user-images.githubusercontent.com/13609011/91695344-f2dfae80-eba8-11ea-9a9b-702192316170.jpeg](https://user-images.githubusercontent.com/13609011/91695344-f2dfae80-eba8-11ea-9a9b-702192316170.jpeg)

- 비선점 스케줄링 : `Interrupt`, `Scheduler Dispatch`
- 선점 스케줄링 : `I/O or Event Wait`

------

**프로세스의 상태 전이**

✓ **승인 (Admitted)** : 프로세스 생성이 가능하여 승인됨.

✓ **스케줄러 디스패치 (Scheduler Dispatch)** : 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것.

✓ **인터럽트 (Interrupt)** : 예외, 입출력, 이벤트 등이 발생하여 현재 실행 중인 프로세스를 준비 상태로 바꾸고, 해당 작업을 먼저 처리하는 것.

✓ **입출력 또는 이벤트 대기 (I/O or Event wait)** : 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력/이벤트가 모두 끝날 때까지 대기 상태로 만드는 것.

✓ **입출력 또는 이벤트 완료 (I/O or Event Completion)** : 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러에 의해 선택될 수 있도록 만드는 것.

### **4. CPU 스케줄링의 종류**

- 비선점 스케줄링 (Non-Preemptive Scheduling)

  1. FCFS (First Come First Served)
     - 큐에 도착한 순서대로 CPU 할당
     - 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어짐
     - 일단 CPU 를 잡으면 CPU burst 가 완료될 때까지 CPU 를 반환하지 않는다. 할당되었던 CPU 가 반환될 때만 스케줄링이 이루어진다. ( aka 비선점형 Non-Preemptive 스케줄링 )
     - 문제점 : convoy effect - 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다.
  2. SJF (Shortest Job First)
     - 수행시간이 가장 짧다고 판단되는 작업을 먼저 수행
     - 다른 프로세스가 먼저 도착했어도 CPU burst time 이 짧은 프로세스에게 선 할당
     - FCFS 보다 평균 대기 시간 감소, 짧은 작업에 유리
     - 문제점 : starvation - 효율성을 추구하는게 가장 중요하지만 특정 프로세스가 지나치게 차별받으면 안되는 것이다. 이 스케줄링은 극단적으로 CPU 사용이 짧은 job 을 선호한다. 그래서 사용 시간이 긴 프로세스는 거의 영원히 CPU 를 할당받을 수 없다.

- 선점 스케줄링

  1. Priority Scheduling

     - 정적/동적으로 우선순위를 부여하여 우선순위가 높은 순서대로 처리
     - 우선순위가 가장 높은 프로세스에게 CPU 를 할당하는 스케줄링이다. 우선순위란 정수로 표현하게 되고 작은 숫자가 우선순위가 높다.
     - 더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다. → aka 선점형 스케줄링(Preemptive) 방식
     - 더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다. → aka 비선점형 스케줄링(Non-Preemptive) 방식
     - 문제점 : Starvation - 우선 순위가 낮은 프로세스가 무한정 기다리는 Starvation 이 생길 수 있음, 무기한 봉쇄(Indefinite blocking) - 실행 준비는 되어있으나 CPU 를 사용못하는 프로세스를 CPU 가 무기한 대기하는 상태
     - 해결책 : Aging 방법으로 Starvation 문제 해결 가능 - 아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여주자.

  2. Round Robin

     - 현대적인 CPU 스케줄링

     - 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 갖게 된다.

     - 할당 시간이 지나면 프로세스는 선점당하고 ready queue 의 제일 뒤에 가서 다시 줄을 선다.

     - `RR`은 CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적

     - `RR`이 가능한 이유는 프로세스의 context 를 save 할 수 있기 때문이다.

     - FCFS에 의해 프로세스들이 보내지면 각 프로세스는 동일한 시간의 

       ```
       Time Quantum
       ```

        만큼 CPU를 할달 받음

       - `Time Quantum` or `Time Slice` : 실행의 최소 단위 시간

     - 할당 시간(`Time Quantum`)이 크면 FCFS와 같게 되고, 작으면 문맥 교환 (Context Switching) 잦아져서 오버헤드 증가

     - 장점 1 : Response time이 빨라진다. - n 개의 프로세스가 ready queue 에 있고 할당시간이 q(time quantum)인 경우 각 프로세스는 q 단위로 CPU 시간의 1/n 을 얻는다. 즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.

     - 장점 2 : 프로세스가 기다리는 시간이 CPU 를 사용할 만큼 증가한다.공정한 스케줄링이라고 할 수 있다.

     - 주의점 : 설정한 time quantum이 너무 커지면 FCFS와 같아진다. 또 너무 작아지면 스케줄링 알고리즘의 목적에는 이상적이지만 잦은 context switch 로 overhead 가 발생한다. 그렇기 때문에 적당한 time quantum을 설정하는 것이 중요하다.

  3. Multilevel-Queue (다단계 큐)

     ![https://user-images.githubusercontent.com/13609011/91695428-16a2f480-eba9-11ea-8d91-17d22bab01e5.png](https://user-images.githubusercontent.com/13609011/91695428-16a2f480-eba9-11ea-8d91-17d22bab01e5.png)

     - 작업들을 여러 종류의 그룹으로 나누어 여러 개의 큐를 이용하는 기법

       ![https://user-images.githubusercontent.com/13609011/91695480-2a4e5b00-eba9-11ea-8dbf-390bf0a73c10.png](https://user-images.githubusercontent.com/13609011/91695480-2a4e5b00-eba9-11ea-8dbf-390bf0a73c10.png)

     - 우선순위가 낮은 큐들이 실행 못하는 걸 방지하고자 각 큐마다 다른 `Time Quantum`을 설정 해주는 방식 사용

     - 우선순위가 높은 큐는 작은 `Time Quantum` 할당. 우선순위가 낮은 큐는 큰 `Time Quantum` 할당.

  4. Multilevel-Feedback-Queue (다단계 피드백 큐)

  ![https://user-images.githubusercontent.com/13609011/91695489-2cb0b500-eba9-11ea-8578-6602fee742ed.png](https://user-images.githubusercontent.com/13609011/91695489-2cb0b500-eba9-11ea-8578-6602fee742ed.png)

  - 다단계 큐에서 자신의 

    ```
    Time Quantum
    ```

    을 다 채운 프로세스는 밑으로 내려가고 자신의 

    ```
    Time Quantum
    ```

    을 다 채우지 못한 프로세스는 원래 큐 그대로

    - Time Quantum을 다 채운 프로세스는 CPU burst 프로세스로 판단하기 때문

  - 짧은 작업에 유리, 입출력 위주(Interrupt가 잦은) 작업에 우선권을 줌

  - 처리 시간이 짧은 프로세스를 먼저 처리하기 때문에 Turnaround 평균 시간을 줄여줌

  1. SRT (Shortest Remaining time First)

  - 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
  - 현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다. → aka 선점형 스케줄링
  - 문제점 : starvation - 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용시간)을 측정할 수가 없다.

### **5. CPU 스케줄링 척도**

1. Response Time
   - 작업이 처음 실행되기까지 걸린 시간
2. Turnaround Time
   - 실행 시간과 대기 시간을 모두 합한 시간으로 작업이 완료될 때 까지 걸린 시간









--------------

#### references

sites : [github1](https://github.com/Dinoryong/Interview_Question_for_Beginner/tree/master/OS), [github2](https://github.com/Dinoryong/tech-interview-for-developer/tree/master/Computer%20Science/Operating%20System), [blog1](https://goodgid.github.io/category/#OS), [blog2](https://m.blog.naver.com/PostList.nhn?blogId=adamdoha&categoryNo=81&listStyle=style1), 

books : [운영체제10th](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791185475578&orderClick=LEa&Kc=), [운영체제와 정보기술의 원리](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158903589&orderClick=LEa&Kc=)

lectures : [kocw1](http://www.kocw.net/home/search/kemView.do?kemId=1046323), [kocw2](http://www.kocw.net/home/search/kemView.do?kemId=1349152&ar=relateCourse), [youtube1](https://youtu.be/zGBm37kze9I?list=PLHqxB9kMLLaOs2BM2KbuvttBYCgDoFm-5)

etc : 

- 스케줄링 목표 : https://jhnyang.tistory.com/29?category=815411
- 프로세스 전이도 그림 출처 : https://rebas.kr/852
- CPU 스케줄링 종류 및 정의 참고 : https://m.blog.naver.com/PostView.nhn?blogId=so_fragrant&logNo=80056608452&proxyReferer=https:%2F%2Fwww.google.com%2F
- 다단계큐 참고 : https://jhnyang.tistory.com/28
- 다단계 피드백 큐 참고 : https://jhnyang.tistory.com/156

- 이미지 : https://raw.githubusercontent.com/gyoogle/tech-interview-for-developer/master/resources/CPU%20%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81.PNG
- 이미지

--------------



