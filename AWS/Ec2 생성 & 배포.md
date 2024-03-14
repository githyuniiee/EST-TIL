## 클라우드 서버

- 클라우드 서비스
    - 인터넷을 통해 `서버/스토리지/데이터베이스/네트워크/소프트웨어/모니터링 등의 컴퓨팅 서비스를 제공하는 것`
    - 서버의 사양을 조정할 수 있으며, 서버/저장소 관리, 보안에 대한 부담을 덜 수 있음

- 클라우드 형태
    - IaaS(Infrastructure as a Service)
        - 인프라를 클라우드 형태로 제공
        - 기존 물리 장비를 미들웨어와 묶어둔 추상화 서비스
        - 가상머신, 스토리지, 네트워크 ,운영체제 등의 IT 인프라를 대여해주는 서비스
        - AWS의 EC2, S3 등
        
    - PaaS(Platform as a Service)
        - 플랫폼을 클라우드 형태로 제공
        - IaaS에서 한번 더 추상화된 개념
        - AWS의 Beanstalk(빈스톡), Heroku(헤로쿠) 등
        
    - SaaS(Software as a Service)
        - 소프트웨어를 클라우드 형태로 제공
        - 구글 드라이브, 드랍박스, 와탭 등
        
    
    ## EC2 서버 접속하기
    
    - EC2 (AWS에서 제공해주는 서버)
        
         “AWS에서 리눅스 서버 혹은 윈도우 서버를 사용합니다” 라고 하면 이 EC2를 의미
        
    
    - EIP 할당
        - EC2 인스턴스도 하나의 서버이기 때문에, IP가 존재
        - 인스턴스 생성시 항상 새로운 IP를 할당하는데, 만약 인스턴스를 중지하고 다시 시작하게 된다면 새로운 IP가 할당
        - 인스턴스의 IP가 매번 변경되지 않고 고정 IP를 가지게 됨
    
    EIP는 생성하고 EC2 서버에 연결하지 않으면 비용이 발생
    
    생성한 탄력적IP는 무조건 EC2에 바로 연결해야하며 만약 더는 사용할 인스턴스가 없을 때도 EIP를 삭제해야함
    
    EC2 접속 실습
    
    - 처음 ssh로 접속할 경우 권한 관련 경고가 떴음
        
        키 파일 권한 변경 !
        
    
    ![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/509331c2-b2d5-480f-a834-1010af7db4be)

    - pem 키 ~/.ssh 디렉토리로 복사
    - pem 키 권한 변경 chmod 600
    - pem 키가 있는 디렉토리에 config 파일 생성
    - 본인이 원하는 Host 등록
    - 생성된 파일 chmod 700으로 권한 설정
    
    권한 600 ⇒ rw- (읽기/쓰기 권한)
    
    권한 700 ⇒ rwx (읽기/쓰기/실행 권한)
    
    권한 변경 후 접속 !
    
    ![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/4a20d942-17ef-411d-a0ef-f50c9e7e6ea7)

    리눅스 서버 생성 시 해야 할 설정들
    
    - JAVA 설치
    - 타임존 변경
        - 기본 UTC 기준으로 셋팅
        - `sudo rm /etc/localtime`
        - `sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime`
    
- HOST NAME 변경
    - sudo vim /etc/sysconfig/network에 들어가
    - HOSTNAME = (원하는 호스트네임)

- 로컬/ 도메인명 변경
    - sudo vim /etc/hosts
    
    ![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/c56411fe-890c-435d-8066-ce43d4a642a0)

    

## AWS EC2 서버에 배포

- EC2 서버에 git 설치 `sudo yum install git`
- git clone으로 프로젝트 저장할 디렉토리 생성 `mkdir ~/app && mkdir ~/app/step1`
- 해당 디렉토리에 git clone

Gradlew로 코드들이 잘 수행되는지 테스트

- `./gradlew test`
- `chmod +x ./gradlew` ⇒ 실행 권한 추가

EC2 서버에 빌드 & 배포

- 빌드 `./gradlew build`  ⇒ 빌드가 정상적으로 완료되었다면 /build 폴더 생성, /build/libs 하위에 *.jar 형태의 파일이 생김
- jar 파일 실행 `java -jar {파일명}.jar`
- 인바운드 규칙 설정

백그라운드에서 EC2 서버 실행하기

- `nohup java -jar {*.jar파일} 2>&1 &`
- 백그라운드에 떠있는 프로세스 확인 `ps -ef | grep java`
- PID를 이용하여 서버 종료 `kill -9 {PID}`
