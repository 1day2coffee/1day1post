## CPU의 구성
	크게 ALU, 제어장치, 레지스터로 구성 됨

## ALU
	계산기. 레지스터로부터 피연산자, 제어장치로부터 제어신호를 받고 레지스터에 결괏값과 플래그를 반환 함.
	플래그 레지스터에 플래그를 반환함으로 다양한 처리 가능(음수, 제로, 오버플로우, 인터럽트)

## 제어장치
	제어신호를 내보내고 명령어를 해석. 제조사마다 구현이 다름

## 제어장치가 받아들이는 것
	클럭 신호: 컴퓨터 모든 부품이 공유하는 작업리듬
	제어 신호: 제어 버스를 통해 받은 신호를 CPU내부 or 외부에 내보내기도 함
	해석해야 할 명령어: 명령어 레지스터로부터 해석할 명령어를 받음
	플래그 레지스터 값: 플래그 레지스터로부터 플래그 값을 받음
		
## 레지스터
	저장소. CPU내부에 존재하므로 상당히 빠름. ALU 계산 결괏값이나 명령어를 저장하고 다른 부품에 전달 함.

## 레지스터 종류
	프로그램 카운터: 메모리에서 가져올 명령어의 주소를 저장
	명령어 레지스터: 메모리에서 읽어들인 명령어를 저장. 제어장치에게 명령어 전달.
	메모리 주소 레지스터: 프로그램 카운터에 있는 정보 저장. CPU는 이 주소를 보고 주소버스를 통해 메모리에 전달
	메모리 버퍼 레지스터: 메모리로부터 데이터버스를 통해 실제 값을 저장.
	범용 레지스터: 데이터와 주소 모두를 저장.
	플래그 레지스터: ALU 결괏값인 플래그를 저장.
	스택포인터: 스택의 꼭대기를 가르킴. 스택주소 지정방식에 사용 됨.
	베이스 레지스터: 메모리의 기준주소를 가리킴. 변위주소 지정방식 중 베이스레지스터 지정방식에 사용 됨. 

## 스택주소 지정방식
	메모리에는 암묵적으로 스택영역이 존재
	스택포인터를 통해 마지막으로 저장된 주소를 알 수 있음

## 변위주소 지정방식
	오퍼랜드(변위)와 특정레지스터 값을 통해 유효주소를 얻어내는 방식.
	상대주소 지정방식: 오퍼랜드 + 프로그램카운터
	베이스 레지스터 지정방식: 오퍼랜드 + 베이스 레지스터의 값

## 명령어 사이클
	기본적으로 인출과 실행이 반복됨
	인출 후 실행 전 메모리에 접근이 필요한 경우 한번 더 인출
	실행 전 인터럽트가 발생할 경우 인터럽트 처리

## 인터럽트
	CPU 작업을 방해하는 신호.
	동기 인터럽트: CPU에 의해 발생. 예외라고 불림
	비동기 인터럽트: 입출력 장치에 의해 발생. 하드웨어 인터럽트라 불림

## 예외
	폴트: 예외처리 직후 중단한 명령어부터 재실행
	트랩: 예외처리 직후 중단한 명령어 다음 명령어부터 재실행
	중단: CPU가 강제로 중단시킬 수 밖에 없는 오류
	소프트웨어 인터럽트: 시스템 호출 시 발생

## 하드웨어 인터럽트
	입출력장치의 알림.
	CPU가 입출력장치의 완료여부를 계속 확인하는 것은 큰 자원낭비이기 때문에 알림을 받고 인터럽트 처리

## 하드웨어 인터럽트 처리순서
	입출력장치가 CPU에 인터럽트 요청신호 전달
	실행사이클이 끝난 CPU가 요청신호 확인
	인터럽트 플래그를 통해 받을 수 있는 인터럽트인지 확인.
	CPU가 현재 작업까지 백업
	인터럽트 백터를 참조하여 인터럽트 서비스 루틴 실행
		서비스 루틴: 인터럽트 처리 프로그램. 메모리에 적재됨.
		백터: 서비스루틴 주소
	서비스 루틴이 끝나면 백업한 것을 복구하여 재개