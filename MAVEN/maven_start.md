# Maven 이란?

## Maven

Maven은 빌드툴이다. 빌드 과정에서의 작업을 효율적으로 할 수 있도록 도와주는 도구이다.

## 프로젝트 생성

cmd에서 아래와 같은 명령을 실행.

    mvn archetype:generate -DgroupId=[도메인명] -DartifactId=[생성할 프로젝트명] -DarchetypeArtifactId=[기반으로 할 프로젝트명]

## 컴파일

cmd 프로젝트 폴더 내에서 아래 명령 실행

    mvn compile

## 패키징

cmd 프로젝트 폴더 내에서 아래 명령 실행

    mvn package

## Build Lifecycle

Maven의 Build Lifecycle은 단계로 구성되어 있다.

- validate
- initialize
- generate-sources
- process-sources
- generate-resources
- process-resources
- <b>compile</b>
- process-classes
- generate-test-sources
- process-test-sources
- generate-test-resources
- process-test-resources
- test-compile
- process-test-classes
- <b>test</b>
- prepare-package
- <b>package</b>
- pre-integration-test
- integration-test
- post-integration-test
- verify
- <b>install</b>
- <b>deploy</b>

굵은 글씨의 단계를 실행하면 자동으로 이전 단계들도 실행하게 된다. 위의 단계는 패키징을 jar로 했을때의 예이고 패키징을 무엇으로 하느냐에 따라서(pom.xml의 내용에 따라서) 단계가 다르다. Maven은 단계별로 plug-in 프로그램을 매핑하여 사용할 수 있으며 pulg-in들은 또 goal이라고 하는 단계를 가지고 있다. pom.xml을 통해 이를 설정할 수 있다.
