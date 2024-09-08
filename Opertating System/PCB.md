__PCB__
=================================================================
프로세스 제어 블록은 운영체제에서 각 프로세스에 대한 중요한 정보를 저장하는 데이터 구조  
PCB를 통해서 운영체제는 프로세스를 효율적으로 관리, 스케줄링할 수 있다.
- - -

### __PCB의 역할__
* 프로세스 정보 저장 : PCB는 각 프로세스의 메타데이터를 저장
    * 메타데이터: 데이터를 설명하는 데이터
        * 프로세스의 상태
        * ID
        * 권한
        * CPU 사용 정보
* 프로세스 관리 : 프로세스가 생성되면 운영체제는 PCB를 만들어 해당 프로세스의 정보를 기록 __(일반 사용자는 접근 불가)__

### __PCB의 구조__
* 프로세스 스케줄링 상태 : 프로세스가 현재 어떤 상태인지를 나타낸다. (준비, 일시중단 등)
* 프로세스 ID (PID) : 프로세스를 구별하는 고유한 번호
* 프로세스 권한: 해당 프로세스가 접근할 수 있는 자원이나 I/O 장치에 대한 정보
* 프로그램 카운터: 다음에 실행할 명령어의 주소
* CPU 레지스터 : 프로세스를 실행하기 위해 필요한 레지스터의 상태 정보를 저장
* CPU 스케줄링 정보: CPU 스케줄러에 의해 중단된 시간 등에 대한 정보
* 계정 정보: 프로세스가 사용한 CPU 시간과 실행한 사용자에 대한 정보
* I/O 상태 정보: 프로세스가 사용 중인 I/O 장치의 목록

### __컨텍스트 스위칭__
컨텍스트 스위칭은 현재 실행 중인 프로세스의 상태를 저장하고, 다른 프로세스를 실행하기 위해 그 상태를 불러오는 과정

![컨텍스트 스위칭](https://velog.velcdn.com/images/sean2337/post/c498ecd3-a8bc-4ecc-bf27-bb52b20939ec/image.png)

* 과정 __(싱글 코어 기준)__
    * 프로세스 A가 실행 중 : 프로세스 A가 CPU를 사용하다가 멈추면, A의 PCB 정보를 저장
    * 프로세스 B 실행 : 프로세스 B의 PCB를 불러와서 실행
    * 다시 A 실행 : 필요한 경우 A의 PCB를 다시 불러와서 A를 실행  

여러 프로세스가 빠르게 전환되면서 마치 여러 프로세스가 동시에 실행되는 것처럼 보인다.  
하지만 한 번에 하나의 프로세스만 실행

### __컨텍스트 스위칭의 비용__
* 캐시 미스
    * 컨텍스트 스위칭이 발생할 때, CPU의 캐시 메모리에서 데이터를 찾지 못하는 상황이 발생할 수 있다.
	* 이런 경우 캐시가 비워지고, 이로 인해 성능이 저하되는 '캐시 미스'라는 비용이 발생

### __스레드에서의 컨텍스트 스위칭__
* 스레드에서도 컨텍스트 스위칭이 발생하지만, 스레드는 스택을 제외한 모든 메모리를 공유
* 스레드 간의 전환은 프로세스 간의 전환보다 더 빠르고 비용이 적다.
- - -
## __정리__
* PCB : 프로세스에 대한 정보를 저장하는 데이터 구조
* 컨텍스트 스위치 : 프로세스를 전환하는 과정, PCB를 사용하여 상태를 저장하고 로드
* 비용 : 캐시 미스 등으로 인해 성능 저하가 발생할 수 있다.
* 스레드 : 스레드 간의 전환은 더 효율적이다.  

이러한 과정을 통해 운영체제는 여러 프로세스를 효과적으로 관리, 사용자에게 원활한 프로그램 실행 환경을 제공