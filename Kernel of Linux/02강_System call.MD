## System call

	멀티유저 시스템에서 한 프로세스가 다른 프로세스 I/O에 접근하는 일을 방지하기 위해 나온 방법
	Shell이 I/O를 사용하려는 순간 Kernel은 CPU를 빼앗음

## System call 순서

	컴파일러가 유저가 작성한 라이브러리(ex. printf())를 호출
	라이브러리에서 system call 호출 sys_write(2)
	Wrapper Routine에서 write에 대응하는 system call number와 함께 Trap 발생
	Kernel이 system call function table에 접근해 function의 시작주소 접근

	cf. Wrapper Routine: 실질적으로 트랩을 발생시키는 공간

## Kernel System Call Function

	어플리케이션과 커널은 서로 독립된 프로그램이므로 데이터를 주고받을 수단이 필요
	커널만이 이러한 수단을 가지고 있음. 커널만 모든 메모리 엑세스가 가능하기 때문
	
## System call number

	system call table의 인덱스 번호로 사용되며 function 주소의 시작값을 불러오는 용도
	컴파일러와 OS를 제작한 회사에서 정하며 변경할 수 없음
	플랫폼 의존적인 단점때문에 보통 system call을 직접 만들지는 않음
	새로운 system call을 만들고 싶다면 파일 디스크럽터(FD)를 활용

## Process Management

	Kernel은 자체적인 Intenal Data Structure을 가지고 있음(하드웨어, 프로세스관리)
	하드웨어 관리를 위한 Data Structure에는 하드웨어 정보가 담겨있음
	프로세스 관리를 위한 Data Structure에는 PCB라는 데이터 구조체가 있음
	이를 통틀어 메타데이터(metadata) 라고 부름. = 데이터를 위한 데이터

## PCB (process control block)

	PID, 프로세스 우선순위, 대기현상, 프로세스 상태, 디스크 내 위치, 상태백터 저장공간 등을 저장한 구조체
	프로세스가 다른 프로세스를 기다리는 동안 PCB의 상태를 적어 놓고 CPU를 반납

## child process

	
	
	