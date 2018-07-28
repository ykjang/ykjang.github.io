---
layout: post
title:  "[AWS] AWS Elastic beanstalk 을 이용한 웹어플리케이션 구축 - 1"
subtitle:   ""
categories: devlog
tags: aws devops awseb eb elastic benastalk 빈스톡 빈즈톡
comments: true
---



### Elastic Beanstalk(이하 빈스톡) 이란?
> 어플리케이션 설정, 생성, 배포, 관리를 빠르고 간단하게 지원해주는 개발자 풀 코스 서비스.   
> 빈스톡, 빈즈톡으로 발음. 일반적으로는 빈스톡으로 사용함.
> 현재 사용되고 있는 대부분의 웹기반 플랫폼을 제공
> 어플리케이션 배포 및 버전 관리와 모니터링 구성을 자동화.


```text
With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications.    
AWS Elastic Beanstalk reduces management complexity without restricting choice or control.    
You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.    
Elastic Beanstalk uses highly reliable and scalable services that are available in the AWS Free Tier.
```


**요약하면,**

> **프로비저닝( Provisioning )의 결정체**


> 인스턴스(EC2) 및 OS 설치, 
> 웹어플리케이션 소프트웨어 구성,     
> 오토 스케일링 구성,   
> 로드 밸런서 구성,
> 업데이트 배포 및 버전 관리,
> 모니터링 관리 설정   
  
> 모두를 빠르게 쉽게 만들어주는 플랫폼 서비스라고 보면 됨.

- 다양한 개발 언어와 플랫폼을 기본으로 제공, 개발자가 서버의 구성부터 어플리케이션의 구성, 또 구성 이후의 업데이트 까지 프로비저닝을 해준다.
- 지원되는 언어 & 플랫폼: Go, Java, Tomcaat, .NET, Node.js, PHP, Python, and Ruby.


#### 빈스톡은 개발자에게 왜 유용한가?
- **프로비저닝** - 아무리 DevOps가 대세인 시대이지만, 개발자가 서버구성부터 OS설치, 컨테이너 설치, 로그설정, 모니터링, 보안구성까지 모두 하기에는 부담스러운게 사실. 클릭 몇번 또는 명령어 몇줄로 구성이 가능.
- **빠른 개발테스트 와 배포** - 빨리 개발된 기능을 테스트해 보고 싶은데 EC2 생성부터 OS설치, JDK, Tomcat... 모두 세팅하기에는 너무 비효율적임. 

#### 빈스톡의 구성
- 어플리케이션(Application) 과 환경(Environment)으로 구성
- 빈스톡은 어플리케이션을 만들고 하위에 환경을 구성함   
- 하나의 어플리케이션에 2개이상 환경을 구성할 수 있음.

- **어플리케이션**
	- 인스턴스의 논리적인 집합, 하위 어플리케이션 버전의 관리    
        - 어플리케이션의 재배포와 이전버전으로의 복원이 가능
	- 폴더의 개념과 유사
- **환경**
	- EC 인스턴스, 로드밸런서, 오토스케일링그룹, 보안그룹의 집합체
	
- 동일한 어플리케이션내에서 환경은 서로 Swap이 가능함.

---

### 빈스톡 환경 (Environment)
- '웹서버 환경'과 '워커 환경' 두가지 환경을 지원

##### 웹서버 환경
- 일반적인 웹어플리케이션, HTTP 기반 API서비스를 구성할때 사용

![](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/aeb-architecture2.png)


##### 워커 환경
-  Amazon SQS를 이용한 메세지기반 백그라운드에서 처리하는 특수 애플리케이션을 구성할 때 사용

![](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/aeb-architecture_worker.png)

---

### 빈스톡 설치방법 및 사용법

빈스톡을 사용하는 방법은 두가지.   

1. AWS 관리 콘솔(AWS Management Console)
2. AWS EB CLI (AWS EB Command Line Interface)를 이용하는 방법이 있음.


빈스톡은 어플리케이션(application)을 만들고. 하위에 환경(environment)을 구성함 하나의 어플리케이션에 2개이상 환경을 구성할 수 있음.

- 어플리케이션: 인스턴스의 집합, 환경에 배포된 어플리케이션 버전의 관리 (재배포, 이전버전으로의 복원이 가능)
- 환경: 인스턴스의 개념 

---

￼
### AWS(AWS Management Console) 관리콘솔을 이용한 EB구성


1. AWS 콘솔 로그인
2. Elastic Beanstalk 메뉴로 이동
3. 새로운 어플리케이션 생성
4. 새로운 환경 구성 (실제 어플리케이션 구성작업) - Tomcat 플랫폼으로 설정
5. 설정 정보 확인 
5. 어플리케이션 소스 배포 - WAR
	6. 배포는 항상 AWS S3를 통해 업로드 되는 방식
	7. 배포버전이 설정한 주기동안 보관되고 어플리케이션 버전관리에서 특정버전으로의 재배포가 바로 가능.
6. 어플리케이션 확인


---

### AWS CLI(Command Line Interface) 를 이용한 EB구성


1. AWSEB CLI 설치
2. AWS 접속정보 및 권한 설정
3. 접속 테스트 
4. 어플리케이션 생성 및 배포


#### 1. AWSEB CLI 설치 (AWS CLI와는 별개)
[AWS EB CLI 설치 메뉴얼 - MacOS](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-osx.html)

- MacOS에는`yum`이나 `apt`대신 Homebrew 이용한다, 없다면 설치방법 구글링 후, brew 사전설치. 
  - `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com. Homebrew/install/master/install)"`
  - brew 최신버전으로 업데이트 - `$ brew update`

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


여기까지 진행했으면 AWS EB CLI를 사용하기 위한 기본적인 준비가 완료됨.   
아래의 참고문서를 참조할 것.

         
---
      
#### 2. AWS 접속정보 및 권한 설정

- CLI 접속을 위해 AWS 콘솔에서 계정생성 및 권한 부여 ( IAM )
- IAM에서 생성된 엑세스 키와 토큰 ( aws_access_key_id, aws_secret_access_key)를 사용해서 접속권한 설정
	- 빈스톡 어플리케이션 초기화(생성): `$ eb init`
	- ID / KEY 등록
- profile 확인 : `$ cat ~/.aws/config`


```
[profile user01]
aws_access_key_id = USER01_ACCESS_KEY_ID
aws_secret_access_key = USER_01_AWS_SECRET_ACCESS_KEY

[profile user02]
aws_access_key_id = USER02_ACCESS_KEY_ID
aws_secret_access_key = USER_02_AWS_SECRET_ACCESS_KEY
```


- 어플리케이션이 생성되었는지 콘솔에서 확인
- 접속권한은 용도에 따라 여러개로 구성이 가능하고, eb 명령어 전체에 `--profile 프로파일명` 옵션을 이용해서 사용이 가능함.
	- my-profile에 만들어진 eb목록을 불러옴 : `$ eb list --profile my-profile`
	

---

#### 3. 어플리케이션 생성 및 배포

1. `$ mkdir HelloWorld`
2. `$ cd HelloWorld`
3. `$ eb init -p PHP`
4. `$ echo "Hello World" > index.html`
5. `$ eb create dev-env`
6. `$ eb open`


---

### [참고문서]


- [빈스톡 소개 동영상](https://www.youtube.com/watch?time_continue=18&v=SrwxAScdyT0)
- [What is AWS Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html)
- [AWS Beanstalk Install Guide](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-osx.html)
- [AWS CLI 설치 메뉴얼 - MacOS](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-install-macos.html)
- [AWS EB CLI 설치 메뉴얼 - MacOS](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-osx.html)