## AWS Elastic beanstalk 을 이용한 웹어플리케이션 구축 -1


###| Elastic Beanstalk(이하 EB) 이란?
> 빈스톡, 빈즈톡으로 발음.  
> 어플리케이션 설정, 생성, 배포, 관리를 빠르고 간단하게 -> 코드 작성에만 집중.  
> 여러 개발 플랫폼을 제공 -  Go, Java, .NET, Node.js, PHP, Python, and Ruby.  
> 어플리케이션 배포 버전관리.    

[영상링크]()

###| 장점

---

- 빠르고 간편한 어플리케이션 시작
- 적절한 규모유지
- 개발자 생산성 
- 완벽한 리소스 제어


한 마디로,

> 웹어플리케이션 소프트웨어 구성,
> 인스턴스(EC2) 구성,
> 용량, 오토 스케일링 구성,   
> 로드 밸런서 구성,
> 업데이트 배포 및 버전 관리,
> 모니터링 관리 설정을  
> 빠르게 간편하게 해주는 서비스라고 보면 됨.

다양한 개발 플랫폼을 기본으로 제공, 개발자가 서버의 구성부터 시작해서 JDK설치,  Apache(또는 Nginx), Tomcat 설치 및 연계,구성등에 신경 쓸 필요가 거의 없슴.


###| 설치방법 및 사용법

---

빈스톡을 사용하는 방법은 두가지.   

1. AWS 관리 콘솔(AWS Management. Console)
2. AWS EB CLI (AWS EB Command Line Interface)를 이용하는 방법이 있음.


***어플리케이션(application)을 만들고. 하위에 환경(environment)을 구성함 하나의 어플리케이션에 여러개의 개별 환경을 구성할 수 있음.***

￼
###| AWS(AWS Management Console) 관리콘솔을 이용한 EB구성
---

1. AWS 콘솔 로그인
2. Elastic Beanstalk 메뉴로 이동
3. 새로운 어플리케이션 생성
4. 어플리케이션 하우에 새로운 환경을 구성 (실제 어플리케이션 구성작업)
5. 어플리케이션 소스 배포
6. 확인



###| AWS CLI(Command Line Interface) 를 이용한 EB구성
---

1. AWSEB CLI 설치
2. AWS 접속정보 및 권한 설정
3. 접속 테스트 
4. 어플리케이션 생성 및 배포


#### 1. AWSEB CLI 설치

- MacOS에는 Homebrew 이용한다, 없다면 설치방법 구글링 후, brew 사전설치. 
  - `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com. Homebrew/install/master/install)"`
  - 홈브루 설치방법 참조링크
  - brew 최신버전으로 업데이트 `$ brew update`

- brew를 이용한 awsebcli 설치
  - `$ brew install awsebcli`
  - 버전확인: `$ eb --version` -> `EB CLI 3.2.2 (Python 3.4.3)`

- 파이썬 설치
  - `$ curl -O https://bootstrap.pypa.io/get-pip.py`
  - `$ python3 get-pip.py --user`
   
- eb 최신버전으로 업그레이드
  - `pip3 install awsebcli --upgrade --user`
- eb 버전체크
  - `$ eb --version`
  - '$ eb --version


여기까지 진행했으면 AWS EB CLI를 사용하기 위한 기본적인 준비가 완료됨.

#### 2. AWS 접속정보 및 권한 설정

#### 2. 접속 테스트

#### 2. 어플리케이션 생성 및 배포







￼

￼
