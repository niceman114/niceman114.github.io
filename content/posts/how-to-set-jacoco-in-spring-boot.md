---
title: "Spring Boot에서 Jacoco 세팅하기"
description: "Jacoco 세팅하는 방법에 대해 기술합니다"
date: 2023-07-12
draft: false
categories:
  - Java
tags:
  - jacoco
  - settings
  - spring boot
  - tdd
  - code coverage
authorbox: true
---

## jacoco가 뭔가요?
Java 프로젝트를 개발하면서 테스트 케이스들을 만들게 되는데, 테스트 Coverage 리포트를 자동으로 생성해 주는 툴입니다.
이름이 왜 `jacoco`인가 했더니, Java Code Coverage의 줄임말이네요. ㅎㅎ
간단한 몇 가지 설정으로 금방 결과물 확인이 가능하니, 아직 망설이고 계신 분들은 꼭 프로젝트에 적용해 보시길 권장 드려요! 😄

## 설정방법: gradle 기준
1. build.gradle 파일을 다음과 같이 변경합니다.
    - As-is
      ```groovy:build.gradle
      plugins {
          id 'java'
          id 'org.springframework.boot' version '2.7.13'
          id 'io.spring.dependency-management' version '1.0.15.RELEASE'
      }

      group = 'how.to'
      version = '0.0.1-SNAPSHOT'

      java {
          sourceCompatibility = '17'
      }

      repositories {
          mavenCentral()
      }

      dependencies {
          implementation 'org.springframework.boot:spring-boot-starter-web'
          testImplementation 'org.springframework.boot:spring-boot-starter-test'
      }

      tasks.named('test') {
          useJUnitPlatform()
      }
      ```
    - To-be: 아래 코드 블럭의 주석 참고
      ```groovy:build.gradle
      plugins {
          id 'java'
          id 'org.springframework.boot' version '2.7.13'
          id 'io.spring.dependency-management' version '1.0.15.RELEASE'
          id 'jacoco' // 필수: jacoco 플러그인을 추가합니다.
      }

      group = 'how.to'
      version = '0.0.1-SNAPSHOT'

      java {
          sourceCompatibility = '17'
      }

      repositories {
          mavenCentral()
      }

      dependencies {
          implementation 'org.springframework.boot:spring-boot-starter-web'
          testImplementation 'org.springframework.boot:spring-boot-starter-test'
      }

      tasks.named('test') {
          useJUnitPlatform()
          finalizedBy jacocoTestReport // 필수: 'test' task가 완료된 직후 'jacocoTestReport' task가 실행되도록 의존 설정을 추가합니다.
      }

      // 필수: jacocoTestReport task 블럭을 추가합니다.
      tasks.named('jacocoTestReport') {
          reports {
              xml.required = false // 옵션(기본값:false): xml 파일을 reports/jacoco/test 경로에 생성
              csv.required = false // 옵션(기본값:false): csv 파일을 reports/jacoco/test 경로에 생성
              html.outputLocation = layout.buildDirectory.dir('reports/jacoco/test') // 옵션(기본값: reports/jacoco/test): html로 된 리포트를 해당 경로에 생성
          }
      }
      ```
1. gralde task 실행: verification > test
  ![gradle의 jacoco tasks가 추가됨](/posts/img/jacoco-gradle-tasks.png#center)
1. 테스트가 종료되면, $BUILD_HOME/reports/jacoco/test 경로에 html 디렉토리가 생성됩니다.
  ![](/posts/img/jacoco-reports.png#center)
1. 이제 index.html 파일을 브라우저에서 오픈하면 됩니다!
  ![](/posts/img/jacoco-reports-html-index.png#center)
## 참고
- 예제코드 : https://github.com/niceman114/how-to-use-jacoco
- jacoco 프로젝트 홈: https://www.jacoco.org/jacoco/index.html
  - 뭔가 너무 올드하지만 절대 위험한 사이트는 아닙니다. :nerd_face: