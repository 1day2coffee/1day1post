## 운영체제(OS)란?

	하드웨어 자원(CPU, Memory, Disk)를 관리하고 프로그램들을 지원해주는 것
	편의를 위해 하드웨어를 감추고 겉으로 다른 프로그램을 지원해줌
	운영체제로 프로그램이며 여러 프로그램들의 모음

## Linux Terminology

	Kernel: 메모리 상주(Memory Resident) 프로그램. 평범한 C 프로그램
	Utility: 디스크 상주(Disk Resident) 프로그램. 유저 요청 시 메모리에 로딩. = Command
	Shell: Utility의 하나로써 많은 프로그램들의 메모리 교통정리 해주는 프로그램. Job Control이 주 목적
	File: sequence of bytes. 리눅스에서는 I/O Device로 file로 취급. /dev 경로에 있음

## Kernel-Shell-Utilities 의 관계

	시스템 부팅을 하면 메인 메모리에 Kernel이 로딩
	유저가 터미널 실행 시 Shell이 메인 메모리에 로딩
	유저가 커맨드를 입력하면 Shell은 이에 대응하는 Utility를 디스크에서 가져와 메모리에 로딩
	cf. 터미널은 콘솔의 부분집합이나 거의 동일한 의미로 사용
	
## Linux vs Windows
	
	철학: single-user vs multi-user
	보안: Yes vs Little
	자원사용: minimize vs use them all
	인터페이스: CUI vs GUI

## Linux Protection
	
	사후처리 대신 사전예방을 목적
	Shell을 포함한 다른 프로그램들이 I/O하는 순간 CPU 사용권한을 뺏음
	I/O 시 Kernel에게 요청하고 Kernel은 작성 된 Function을 수행하게 함(System calls)

## Mode bit
	
	Linux는 System call을 위해 CPU에 하나의 Binary bit를 도입.
	Mode bit 1일 경우 모든 memory access 가능 (kernel mode)
	Mode bit 0일 경우 그 유저의 address space만 접근 가능 (user mode)
	Kernel mode일때 모든 Instruction 가능, User mode일때는 제한

## Machine Instruction Cycle

	PC to memory - Instruction Fetch - Decode - Execute - Increment PC

	User mode 일 때,
	CPU는 작업을 위해 계속 메모리에게 PC에 있는 address를 보냄
	CPU와 메모리 사이에는 MMU가 있어 address정보를 조사하고 올바른지 판단. 통과 시 Instruction Fetch 실행. op-code, operands 확인.
	privileged op-code면 CPU 뺏음

## C언어가 동작하는 과정

	Source에 printf 작성 및 컴파일
	컴파일러가 chmodk instruction 실행 
	CPU 뺏음. H/W trap에 걸림
	Trap handler routine으로 진입(mode bit 1)
	Parameter를 보고 알맞은 명령어로 처리
	명령어 처리 후 Trap으로 돌아감(mode bit 0)

## every program needs two stacks

	프로그램은 커널모드와 유저모드가 계속 반복됨
	function에는 지역변수들이 있기 마련. 따라서 이에 대응하는 자료구조가 필요함
	function이 call되고 return되기까지 존재해야하므로 stack을 사용 함
	유저모드에서 유저만의 function을 위해서, 커널모드에서 커널의 function을 위해 stack이 2개 필요 함


