# OS (Operating System)

![](https://cdn.ttgtmedia.com/rms/onlineimages/whatis-how_operating_systems_work_half_column_desktop.png)     

출처 : https://whatis.techtarget.com/definition/operating-system-OS

<br/>

- 운영체제
- 컴퓨터의 사용자와 하드웨어 사이에서 중개자 역할을 해주는 프로그램
- 사용자의 언어를 컴퓨터가 이해할 수 있는 언어로 번역해준다.
- 응용 프로그램을 실행시키고, 사용자의 입/출력을 제어한다.

<br/>

## 운영체제의 목적

- 사용자가 컴퓨터를 편리하게 사용
- 하드웨어(CPU)의 효율적인 사용

<br/>

## 운영체제의 역사

1. 프로그램마다 전선을 갈아끼우면서 사용 (수작업) -> 
2. 단일 프로그래밍 (한 번에 하나의 프로그램만 실행) ->
3. 다중 프로그래밍 (한 번에 vs code, 계산기, 메모장 등 여러 프로그램 실행) & 시분할 (여러 프로그램이 동시에 실행되고 있을 때, 해당 프로그램이 CPU에 할당되는 시간을 잘게 쪼개 분해하여 사용자가 느끼기에 동시에 여러 프로그램이 돌아가고 있다고 느끼는 것) -> 
4. 모바일 OS & 실시간 시스템

<br/>

### 1. Batch System ( 일괄처리 시스템 )

![](https://qph.fs.quoracdn.net/main-qimg-b4f284e32c384b097bb93849e695e6a6.webp)     
출처 : https://www.quora.com/What-is-a-batch-operating-system-time-sharing-operating-system-distributed-operating-system-network-operating-system-and-an-embedded-system

<br/>

비슷한 작업을 주기적으로 묶어 한 번에 처리. 기계적인 입출력 장치의 속도가 CPU 같은 전자적 장치의 속도보다 느리기 때문에 CPU가 계속해서 쉬는 상태(idle)인 경우가 많다.

<br/>

### 2. Multi-Programed System ( 다중 프로그램 시스템 )

![](https://imgs.developpaper.com/imgs/3574004475-5d8a11aa1b19e_articlex.jpg)     
출처 : https://developpaper.com/operating-system-learning-1-understanding-operating-system-design-requirements-from-the-development-history/

<br/>

CPU가 처리할 작업이 항상 있도록 하는 방식. 메모리 내에 있는 작업들을 하나씩 실행하다가, 실행중인 작업이 입출력 등에 의해 기다리는 상태가 되면 다른 작업으로 넘어가 작업을 계속 실행한다. 이 후 첫번째 작업이 끝나면 현재 작업을 중단하고 다시 첫번째 작업이 CPU를 차지하게 되는 방식이다.

<br/>

### 3. Time Sharing System ( 시분할 시스템 )

![](https://ecomputernotes.com/images/Time-Sharing-System-Active-State-of-User-5.jpg)     
출처: https://ecomputernotes.com/fundamental/disk-operating-system/time-sharing-operating-system

<br/>

- CPU 는 한 번에 하나의 일만 처리할 수 있다.     
그러나 시분할 시스템은 프로그램이 실행되고 있을 때 매우 짧은 주기로 CPU 를 각 프로그램에 할당해 주기 때문에 사용자는 모든 프로그램이 동시에 동작한다고 느끼게 된다.

- Liunx : 시분할 시스템을 사용. 여러 명의 사용자가 동시에 하나의 컴퓨터에 접속해서 서로 다른 처리를 할 수 있다.

<br/>

`오늘 공부한 내용`
- https://www.youtube.com/watch?v=EAoJb00Iwso
- https://youtu.be/wQsFUuC9TBs