리눅스마스터 1급
1차 - 필기 4지선다 100문항 과목평균 60점 / 40점 과락
시험비 4만원
시험시간 100분



출제기준
1. 리눅스 실무의 이행
리눅스의 개요 - [운영체제 개요 / 리눅스 기초]
리눅스 시스템의 이행 - [리눅스와 하드웨어 / 리눅스의 구조 / X 윈도우 / SHELL / 프로세스]
네트워크의 이행 - [네트워크 기초 및 설정]
2. 리눅스 시스템 관리
일반 운영관리 - [사용자, 파일시스템, 프로세서, S/W설치 및 관리]
장치관리 - [장치의 설치 및 관리 / 주변장치 관리]
시스템 보안 및 관리 - [시스템 분석 / 시스템 보안 및 관리 시스템 백업]
3. 네트워크 및 서비스의 활용
네트워크 서비스 - [웹, 인증, 파일, 메일, DNS관리(설치 및 설정) / 가상화 관리 및 기타 서비스]
네트워크 보안 - [네트워크 침해 유형 및 특징 / 대비 및 대처 방안]





------------------------------------------------------------------------------------
옵션에 i가 대문자 인지 소문자인지
리눅스 역사
ext4의 파티션 넘버 고르기
ext4의 파티션 넘버
리눅스 역사
실기시험은 시험장가면 리눅스 들어있는 USB를 주고 그걸로 부팅해서 설정값이나 이런걸 확인해서 답안지에 답을 쓰는 형식
자격증 합격자 블로그 정보

1과목 부분에서 잡아야 할 필수 개념 부분

라이센스의 종류와 특징, 차이점
리눅스 배포판의 특징
X윈도우
시그널 개념 - 보는 법, 번호
IP - 서브네트워크, 호스트 수
클라우드
사물인터넷
빅데이터
임베디드
가상콘솔
스와핑
가상메모리

관련 포스팅 링크:
♣ 오픈소스 소프트웨어 라이선스
오픈소스 SW라이선스(license) 종류, 특징, 설명
♣ 리눅스 배포판
리눅스 OS 배포판 종류와 역사, 특징, 목적, 추천 등 (우분투, 데비안, 페도라, CentOs, 레드햇, 슬렉웨어 등등)
♣ 시그널
시그널이란? 시그널 (SIGNAL) 종류, 상황, 유사 시그널 차이점
2과목 부분에서 잡아야 할 필수 개념 부분

사용자 추가하기 - useradd
사용자 비번 바꾸기 - passwd
사용자 정보 변경하기 - usermod
clone 문제
tar - gzip / bzip2인지 옵션에 따라서 파악하기
module관련 명령어 - insert module 인 insmod 제거하기 - remove module / rmmod / modprobe
파일 갱신돕는 depmod
백업 dump / dd

관련 포스팅 링크:
♣ 사용자 관리

♣ 파일 묶기 tar
파일 묶기와 압축하고 풀기- tar 명령어와 옵션, 사용법, 제외하고 묶기, 묶고 파일지우기
♣ 크론
3과목 부분에서 잡아야 할 필수 개념 부분

DNS랑 보안 꼭 몇문제씩 나오더라

DNS는 뭐 이해안되도 걍 외우는게 답일 때가 있어
괄호에 뭐가 들어갈지 묻는 문제가 많이 나오는 데 개념까진 모르더라도 답 맞추기 쉬우니까 암기하고가..

1

2

3

4
1902회 여기서만 괄호채우는거 이렇게 4개 나옴;;;;; 말 다했죠ㅎ
그리고 DNS다음으로는 mail쪽 많이 나오는거같아요. aliases부분, access 파일 부분 등, 언제 설정하고 특정 설정 후에는 어떤 명령어로 반영시켜줘야 하는지 등... 알아두기~

iptables~ 미친듯이 단골~~ 네 걍 단골

그리고 디도스 공격 종류와 특징에 대해서 암기하기 어렵지 않으니까 시험보기 전에 꼭 머리속에 넣기! 꼭 나옴


---------------------------------------------------------------------------------------------------------------


리눅스마스터 1급 책정리

Part1 리눅스 일반
리눅스 개요
리눅스의 탄생 - [1989년 리누스 토르발스가 개발한 Unix를 기반으로 개발하였으며 오픈소스 운영체제이다]
특징 - [ Multi(user / tasking / processor / platform), 계층형 파일시스템, POSIX와 호환, 네트워킹 기능, 가상콘솔, virtual memory ] 
다중 유저 - 동시에 여러명의 유저가 접속해서 컴퓨터 시스템 이용가능 / 사용자별 권한관리와 자원관리가 가능해서
다중 프로세스 - A Multi processor is a computer system with two or more central processing units(CPUs) share full access to common RAM
다중 작업 - 운영체제 내에서 여러개의 프로세스를 동시에 실행시켜 CPU 스케줄링하여 동시에 작업을 하는 것.
다중 플랫폼 - 여러 회사의 CPU를 지원한다.
ROOT를 기반으로한 트리형태의 계층형 파일 시스템 구조
POSIX - 유닉스 시스템의 표준 인터페이스
네트워킹 - TCP/IP, IPX/SPC, Appletalk, Bluetooth, Gateway, Subnet
가상콘솔 - 기본적으로 6개의 가상콘솔이 있어 창마다 서로 다른 작업을 수행할 수 있다.
Virtual Memory - Main Memory의 용량적 한계를 극복하기 위해 보조기억장치를 Main Memory 처럼 사용하는 방법 
철학 
GPL - General Public License [GUN 철학]
출시되는 모든 소프트웨어는 무료이다.
어느 누구도 이 자유를 뺴앗을 수 없다.
소프트웨어를 다시 수익을 위해 판매할 수 있다.
판매자는 변경한 내용과 모든 소스코드를 전부 공개한다.
LGPL
Library/Lesser Genral Public License - 소스코드를 수정할때 파생된 저작물에 대해서 라이브러리 소스코드를 제공하는 것.
BSD - Berkeley Software Distribution - 버클리 캘리포니아 대학에서 배포한 공개 소프트웨어 라이센스
누구나 수정 배포 가능
수정본의 재배포는 의무가 아님
2차적 파생물에 대한 원시 소스코드에 대해 비공개 가능
MPL (Mozilla Pulic License) 
모질라 재단
GPL + BSD
소스코드를 수정할 때 소스코드를 공개해야된다.
MPL소스코드와 다른 코드를 결합하여 개발할 경우 공개하지 않아도 된다.
GUN (GUN's not Unix)
리차드 스톨만 - Unix 운영체제와 완전한 호환성을 가진 소프트웨어 개발목적으로 소프트웨어를 공유한 최초의 공동체
freeware  - 금전적 권리포기하고 누구나 완전무료사용
shareware - 공개소프트웨어로 일정기간 동안 무료 이후부터 유료
장점과 기능
이식성 - 대부분 C언어로 개발, 일부 어셈블리로 개발 => C언어는 특정기계에 의존적이지 않음 => 어떤 시스템에도 적용가능
개발환경 - C와 Java같은 언어를 지원
네트워크 - ftp, telnet, ssh, 웹서버, 웹 어플 서버, DB 서버 등 구축용이
보안성 - iptables, ssh
다양한 주변 하드웨어 지원
우수한 성능 - 고가의 유료 유닉스 서버와 동일한 성능 
신뢰성 - ext4 파일시스템과 fsck를 통한 파일 시스템 무결성 검사 / RAID를 통한 디스크 장애시 복구 기능
종류
레드햇
데비안
수세
칼데라
맨드레이크
슬랙웨어
VM으로 리눅스 구동
MAC에서 가상머신으로 리눅스 구동하기
Boot Master
LILO (Linux Loader) - 리눅스의 부트로더
/etc/lilo.conf
GRUB
/boot/grub/grub.conf
설정값
defaul
timeout
splachimg
hiddenmeun
title Fedora
특징
부트정보를 사용자가 임의 변경 가능
운영체제 멀티부팅가능
커널 경로 및 파일명만 알고 있다면 부팅이 가능
부트로더(Boot Loader)
리눅스 디렉토리 구조
/
bin                - 기본적인 실행명령
boot             - 부팅에 관련된 파일
dev               - 장치 파일모음
etc                -시스템 설정파일
home            -사용자 홈 디렉토리
lib                 -C라이브러리 파일 / shared lib
lost+found    - 손상된파일들
misc               - 여러가지 잡다한 파일들
mnt                -mounted files
proc               -directories and files that report system status
root                - 루트 사용자의 홈 디렉토리
sbin                - system administration programs 시스템관리 프로그램
tmp                - 임시파일
usr                  - 애플리케이션이 설치되는 디렉토리
var                   - Log files, spool files, and other dynamic files
/usr 디렉토리 구조
X11
booaX11R6t
bin
doc
etc
games
indude
info
local
man
mnt
sbin
share
proc
/dev 디렉토리 구조
fd
had
sda
cdrom
mouse
hdb
hd
/proc 디렉토리 구조
buddyinfo
cmdine
cpuinfo
devices
diskstats
dma
filesystems
interrupts
iomem
ioport
kallsyms
loadavg
locks
mdstat
meminfo
modules
partitions
slabinfo
swaps
uptime 
리눅스 구조 및 명령어
리눅스 사용자 관리
사용자계정
명령어 : useradd
파일 : /etc/passwd
파일 : /etc/shadow
명령어 : su
명령어 : ls -alp
파일 : .bashrc  /  .bash_profile  /  .bash_logout
사용자가 로그인 로그아웃 할때의 환경설정 파일
파일 : /etc/default/useradd
사용자가 추가되면 사용자에 대한 기본적인 정보를 가지고 있는 파일
파일 : /etc/login.defs
명령어 : chage
사용자 패스워드 만료일 설정가능
사용자 패스워드
파일 : /etc/passwd
파일 : /etc/shadow
파일 : sulog
사용자 계정 변경로그
명령어 : su
C : usermod
C : userdel
C : useradd
F : /etc/group
F : /etc/group
F : /etc/gshadow
C : groupmod
C : groupdel
C : users, who, w, id, groups, last
F : wtmp
리눅스 시스템 구조
리눅스 시스템 구조
커널
셸
파일 시스템
리눅스 파일 시스템
부트블록
슈퍼블록
아이노드
데이터 블록
파일시스템 생성
fdisk
mkfs
fsck
mount
리눅스 관련 명령어
cd, pwd
ls
history
alias
redirection
pipe
cron
quota
하드 디스크 용량 정보
파일압축
명령어 확인
디렉토리 및 파일관련 명령어

다중프로세서 


리눅스 운영 및 관리
