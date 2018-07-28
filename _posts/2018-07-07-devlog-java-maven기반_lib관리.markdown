---
layout: post
title:  "[Java/Maven] Maven기반 빌드환경에서 로컬라이브러리 추가방법"
subtitle:   "Maven기반 프로젝트 관리"
categories: devlog
tags: java
comments: true
---

### [Java/Maven] Maven기반 빌드환경에서 로컬파일 빌드시 추가방법


Naven기반으로 라이브러리 및 의존성관리를 하다보면 간혹,   
[MVN-Maven원격중앙저장소](https://mvnrepository.com/)에 올라와 있지 않은 라이브러리들이 있는데   
이런 라이브러리들은 어쩔 수 해당 사이트에 가서 필요한 버전의 라이브러리 파일을 받아 로컬에서 관리해야 한다.

Maven기반으로 관리되는 라이브러리의 경우 파일들은 `~/.m2/repository` 폴더에 존재하게 되고 버전에 따른 의존성 관리가 된다.   

**웹어플리케이션 프로젝트** 기반에서 배포를 위해 빌드를 수행하면   
이 폴더를 참조하여 의존성 관리에 의해 필요한 lib파일들이 `{프로젝트루트}/WEB-INF/lib`로 이동 - 정확히는 복사 - 된 후, war 파일로 패키징이 된다.

여기에 속하지 않는 로컬파일들,   
즉 위에서 얘기한 MVN에 올라와 있지 않는 별도의 라이브러리,   
또는 커스터마이즈한 라이브러리 파일들을 빌드시에 WEB-INF/lib에 포함시키기 위한 설정이다.

---

`POM.xml` - Maven 설정파일- 파일에 아래와 같이 plug-in tag를 추가한다.

##### POM.xml 파일 추가항목
``` xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-war-plugin</artifactId>

    <configuration>
        <webResources>
            <resource>
                <!-- 로컬 lib파일 경로 -->
                <directory>${project.basedir}/local-repo</directory>
                <includes>
                    <include>추가할라이브러리.jar</include>
                    ...
                    ...
                </includes>
                <targetPath>WEB-INF/lib</targetPath>
            </resource>
        </webResources>
    </configuration>
</plugin>
```

Team-Share 프로젝트인 경우,   
${project.basedir}아래의 폴더는 멤버모두 생성을 해 놓은 약속된 폴더여야 한다.   
`<directory>`의 경로는 팀과의 프로젝트를 공유하는 환경에서는 절대경로를 사용하지 않아야 한다.

이렇게 수정한 후,
`mvn package`를 하면 지정된 폴더에, 지정된 파일들이 `<targetPath>`에 지정된 경로, 
즉 `WEB-INF/lib` 폴더로 복사, 이동하게 된다.

실제로 많이 발생하는 케이스는 아니지만   
`ojdbc.jar` - 오라클 JDBC 라이브러리 - 의 경우,   
사용하고 하는 오라클 버전의 JDBC라이브러리가 MVN에 올라오지 않아,   
오라클 사이트에서 버전에 맞게 다운받거나, 사용하는 오라클DB솔루션에 포함되어 있는 lib를 추출하여   
로컬저장소에 등록하고 사용하는 경우가 많다.