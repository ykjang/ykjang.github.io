
---
layout: post
title:  "[AWS] AWS CLI(Command Line Interface) 구성"
subtitle:   ""
categories: devlog
tags: aws devops cli profile configure
comments: true
---


### AWS CLI 초기설정

aws cli가 정상적으로 설치되면 `~/.aws` 폴더가 생성된다.  
앞으로 설정할 초기설정들과 접속정보 프로파일의 추가는 이 폴더에서 생성되는 `config`와 `credentials`파일을 통해 처리된다.


#### 1. 기본 접속정보

AWS CLI를 설치하고 나면 실제로 AWS에 필요한 계정으로 접속하기 위해   
접속정보와 환경을 설정하는 절차를 아래의 명령을 통해 처리해야 한다.

`$ aws configure`

엑세스 정보와 기본 리전 및 CLI로 요청한 정보를 출력할때의 포맷등을 설정한다.

엑세스 정보는 자신의 AWS계정정보에서 확인할 수 있으니 AWS 콘솔 매니저로 접속해서 IAM(Identity and Access Management))메뉴로 이동해서 확인하면 된다.   
아직 키 발급을 하지 않은 상태이면 키 생성을 하도록 하자.

IAM에 대해서는 아래의 링크를 통해 자세한 정보와 설정방법을 확인할 수 있다.

[IAM이란?](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/introduction.html)  

```
AWS Access Key ID [None]: ****
AWS Secret Access Key [None]: *****
Default region name [None]: ap-northeast-2
Default output format [None]: json
```

서울지역이니 무조건 `ap-northeast-2`로 적으면 되고    
출력포맷은 일반적으로 `json`으로 설정하면 된다.

`-- profile [프로파일명]` 옵션으로 프로파일을 지정하지 않았기 때문에 디폴트 프로파일로 설정된다.
따라서 aws cli의 명령행에 프로파일을 지정하지 않으면 이 설정정보로 접속하게 된다.


#### 2. 프로파일 추가

필요에 따라 기본 프로파일이외의 프로파일을 설정해야 할 때가 있다.  
특히 권한별로 여러 계정을 두고 사용하거나, 개발과 상용계정을 같이 사용해야 할때는 프로파일을 추가로 설정해야 한다.

위에서 설명한 명령어를 통해 설정하는게 정석이나
이미 초기 설정하면서 만들어진 파일- `config`, `credentials` 에 필요한 항목을 직접 추가하는 방법도 있다.

사실, 대부분의 서비스가 국내에서 사용되는 경우라면 엑세스키외에는 동일한 정보이다. 
굳이 위의 명령으로 똑같은 정보를 일일히 타이핑 할 필요는 없다.

우선 `config` 파일을 vi 편집기로 열자

```
[default]
region = ap-northeast-2
output = json

```

처음 설정하고 프로파일을 추가하지 않은 상태라면 위의 파일처럼 default정보만 설정되어 있다.

AWS 서비스 지역과 출력포맷이 동일하면 아래와 같이 
그대로 복사해서 프로파일명만 지정해준다.

```
[default]
region = ap-northeast-2
output = json

[profile 프로파일명]
region = ap-northeast-2
output = json

```

추가할 프로파일로 접속할 계정의 엑세스정보를 등록하기 위해 `credentials` 파일을 열고 위에서 추가한
프로파일명으로 자격증명을 추가해준다. 물론 추가할 계정에 대한 엑세스키는 AWS의 콘솔 매니저에서 IAM메뉴를 통해 생성해 놓은 상태여야 한다.

```
[default]
aws_access_key_id = *******
aws_secret_access_key = ********

[프로파일명]
aws_access_key_id = ******
aws_secret_access_key = ****
```

프로파일이 추가되었다.   
확인해보자.

`$ aws ec2 describe-instances --query 'Reservations[*].Instances[*].PublicDnsName[]'`

위 명령행을 실행하면 디폴트 프로파일 계정으로 생성된 **EC2** 인스턴스 목록을 DNS정보만으로 JSON포맷으로 출력해주게 된다.   
원하는 정보가 출력되는지 확인하자.

```
[
    "ec2-******.ap-northeast-2.compute.amazonaws.com",   
    "ec2-******.ap-northeast-2.compute.amazonaws.com",   
    "ec2-******.ap-northeast-2.compute.amazonaws.com",   
    ......,
    ...
]
```

`$ aws ec2 describe-instances --query 'Reservations[*].Instances[*].PublicDnsName[]' --profile 프로파일명`

추가한 프로파일명으로 실행해서 해당 계정의 EC2정보가 조회되는 확인해보자.

앞으로 프로파일 추가 및 수정은 이 두개의 파일을 이용해서 작업하면 된다.

[관련링크](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)

