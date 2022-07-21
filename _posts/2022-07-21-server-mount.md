---
title:  "SERVER MOUNT"
excerpt: "NAS 서버와 마운트 이해 및 설정"

categories:
  - Angular
tags:
  - [Angular, HTTPClient]

toc: true
toc_sticky: true
 
date: 2022-07-18
last_modified_at: 2022-07-18


---
### NAS 서버의 이해
Network Attached Storage 의 약어로 파일을 저장하고 편리하게 이동하기 위해 만들어진 장치.

한장소에 NAS 하드웨어 장치를 두고 네트워크 연결을 통해 언제 어디서 눵하는 파일에접근하거나 공유할수 있도록 만드러짐. (네크워크서비스와 하드웨너 장치 전체를 범주에 두고 NAS 라고 한다.) 
###  MOUNT의 이해
실제공간인 디스크를 사용하기 위해 사용되는 운영 체제에 연결하는것 장치와 파일을 연결 (디스크 공간과 디렉토리를 연결 하는것)

EXAMPLE
USB 사용시 USB 파일이 자동으로 뜨며 연결된다 이는 윈도우에서 자동으로 마운트하여 일어나는 현상이다.

마운트 사용시 주의 사항
한개의 장치에는 한개의 마운트 만을 사용(1:1)
마운트 포인트는 임의의 디렉토리여야함
반드시 포맷(파일시스템 생성)후 사용
마운트 해제시 , 마운트 포인트 이외의 디렉토리에서 해야한다.
마운트 할경우 마운트 포인터의 기존 내용을 덮어버리게 된다.(지워지지는않는다)
사용자 및 시스템 관련된 디렉토리를 마운ㅌ 포인트로 지정해서는 절대 안된다.
마운트시 작업할대상은 반드시 파티션(primary,logical)만 가능, 하드디스크와 확장파티션(extend)는 작ㄹ업대상이 될수없다.

마운트 사용을 위한 과정
1. 디스크 추가
2. 디스크 파티션 분할 (사용할 시스템에 맞춰서 파일 시스템 타입 정하기)
3. 용도에 맞게 파일 시스템 포맷
4. 디스크를 마운트할 마운트 포인트 (디렉토리)를 만들어 놓아야 함(파일은 불가능, 디렉토리만 가능)

NAS 서버를 연결 하기 위한 명령어

1.마운트 패키지 설치 - mount하고자 하는 서버에 samba와 cifs를 설치한다.
#yum install samba
#yum install cifs-utils
2.NAS와 연결(마운트)랑 디렉토리 생성
#sudo mkdir '마운트할 디렉토리명'
3. 일시적인 연결방법 - mount
#mount -t cifs -o user='사용자명',password='암호' \\\\서버주소\\공유폴더경로 /마운트경로
smb 버전을 지정하여 설정 하는 방법
#mount -t cifs -o user='사용자명',password='암호',ver=1.0 \\\\서버주소\\공유폴더경로 /마운트경로
4. 영구적인 연결 방법 - fstab 편집
#vi /etc/fstab
내용 01. \\\\서버주소\\공유폴더경로 /마운트경로
내용 02. //IP/디렉토리명-/마운트할 디렉토리명-cifs-rw,auto,file_mode=0600,dir_mode=0700,uid='USERID',gid='USERID',username='ID',password='비번',vers1=1.0 또는 vers=2.0-0-0
저장후 재부팅하면 /etc/fstab을 마운트 한다. 지정하지 않고 확인 하는 방법은 "mount-a"를 통해 /etc/fstab 을 마운트 하고 "df"를 통해 마운트 되었는지 확인.

fstab 편집 참고
fstab 내부에는 아래와 같은 명칭들이 있고 차례대로 입력해야 한다.
<file system> <mount point> <type> <options><dump><pass>

1. file system - 사용할 disk uuid, 원격IP/디렉토리명
2. mount point - 물리적인 디스크를 디렉토리에 연결하기 위한 설정
3. type - 파일 시스템 종류,  파티션 생성시 정한 파일 시스템 종류 입력
4. options - 파일 시스템에 맞게 옵션 설정 
(중요) 아이디와 비번은 별도의 증명 파일로 대체가능
tkdyddldb : commend 라인에서 직접적으로 표시되는게 아니라 변수 형태로 입력되기 떄문에 유출 가능성이 낮아짐 
사용자홈 , 관리자홈 등 어디엔가 파일 생성
$ vim credentails (파일명은 자유)
username=ID
password= 비밀번호
저장
fstab 에서 username, password 대신에 credentails=/만드경로/credentials dlqfur
5. dump - 백업 설정 (0: 지원안함 , 1: 지원)
6. pass - file sequence check option
fsck 에 의한 무결성 검사 우선순위
0: 무결성 검사 하지않음
1: 우선순위 1위(대부분 root가 설정됨)
2: 우선순의가 2위
//IP/디렉토리명-/마운트할 디렉토리명-cifs-rw,user,auto,file_mode=0600,dir_mode=0700,uid='USERID',gid=root,username='ID',password='비번'-0-0

