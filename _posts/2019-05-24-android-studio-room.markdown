---
layout: post
title:  "[Android Studio] Database room"
date:   2019-05-16 16:04 :07
categories: android
tags: android
image: 
---
# Android Sutdio Room 

## Room이란
- ROOM은 ORM(Object Relational Mapping) 라이브러리이다
- 데이터베이스의 객체를 자바 또는 코틀린 객체로 매핑해주는것
- SQLite의 추상레이어 위에 제공하고 있으며 SQLite의 모든 기능을 제공하면서 편한 데이터베이스의 접근을 허용한다
- 다양한 Annotation을 통해 컴파일시 코드를 자동으로 만들어 준다
- LiveData, RxJava와 같은 Observation 형태를 지원한다
- MVP, MVVM과 같은 아키텍쳐 패턴에 쉽게 활용할 수 있다


## Room과 SQLite의 차이점
 - SQLite 경우 쿼리에 대한 에러를 컴파일에 확인하는것이 없지만 ROOM에서는 컴파일 도중 SQL에 대한 유효성을 검사 가능
 - Schema가 변경이 될경우 SQL쿼리를 수동으로 업데이트 해야하지만 ROOM의 경우는 쉽게 해결이 가능
 - SQLite 경우 Java데이터 객체를 변경하기위해 많은 상용구 코드(Boiler Plate code)를 사용해야하지만 ROOM의 경우 ORM라이브러리가 상용구 코드(Boiler Plate code) 없이 매핑 가능합니다.
    - Boiler Plate code : 수정하지 않거나 최소한의 수정만을 거쳐 여러곳에 필수적으로 사용되는 코드
- ROOM의 경우 LiveData와 RxJava를 위한 Observation 으로 생성하여 동작할 수 있지만 SQLite는 그렇지 않다.

## Room의 구성요소
Room의 Component는 세가지 `Entity, DAO, Database`가 있다.
- Database
    - 데이터베이스 보유자
    - database holder를 포함하며, 앱에 영구 저장되는 데이터와 기본 연결을 위한 주 액세스 지점
    - RoomDatabase를 extends 하는 추상 클래스여야 하며, 테이블과 버전을 정의하는 곳
- DAO (Data Access Object)
    - 데이터베이스에 접근해서 실질적으로 insert, delete 등을 수행하는 메소드를 포함한다
- Entity
    - Database 안에 있는 테이블을 Java나 Kotlin 클래스로 나타낸 것이다
    - 데이터 모델 클래스라고 볼 수 있다
    - Database 내의 테이블을 뜻한다

## Dependency 추가
`build.gradle`에 디펜던시를 추가한다
~~~
dependencies {
    implementation "android.arch.persistence.room:runtime:1.1.1"
    annotationProcessor "android.arch.persistence.room:compiler:1.1.1"
    testImplementation "android.arch.persistence.room:testing:1.1.1"
}
~~~

## Database 정의




## 출처
-  https://namget.tistory.com/entry/안드로이드-ROOM-라이브러리-사용하기-코루틴 [남갯,YTS의 개발,일상블로그]