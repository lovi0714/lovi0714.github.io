---
title : "트리거(Trigger)와 프로시저(Procedure)"
excerpt : "차이점을 알아보자"

categories:
- DB
tags:
- [DB]

toc: true
toc_sticky: true

date: 2023-03-01
last_modified_at: 2023-03-01
---

# ✔ 트리거(Trigger)와 프로시저(Procedure)

+ '트리거를 건다', '프로시저'를 실행한다.
+ 프로시저가 함수이고 트리거는 어떤 이벤트에 반응한다 정도로 알고 있었는데 둘의 차이점을 제대로 몰라서 비슷한 거라고 생각했다.
+ 오늘 장애처리 중에 프로시저가 제대로 실행되지 않아서 해결했는데, 사실 트리거인 줄 알고 처리 후에 설명을 했던 것 같아서 더 찾아보고 정리해두려고 한다.

## 📌 트리거(Trigger)
+ 어떠한 트랜잭션이 일어날 때, 반응하여 다른 명령을 실행하게 하는 기능을 하는 것
+ 테이블에 대한 이벤트(INSERT, UPDATE, DELETE)에 반응하여 자동으로 실행되는 코드
+ DDL, DML, 또는 일부 DB 작업(LOGOFF, SHUTDOWN)

### 장점
+ 데이터 무결성 강화 (참조 무결성)
+ 검사 기능의 확장
+ 사용자 편의성 제공
+ 효과적인 데이터 보관

### 단점
- 유지보수의 어려움 (문서화 하지 않는다면, 중간 투입된 개발자들은 파악 어려움)
- 과도한 사용 시 복잡한 상호 의존성을 야기 
- 하나의 트리거가 활성화 --> 이 트리거 내의 SQL문 수행 --> 그 결과로 다른 트리거를 활성화 --> 그 트리거의 SQL 문 수행 --> 반복 (대규모 데이터베이스에서는 관리가 어려움)



## 📌 프로시저(Procedure)
+ 저장프로시저, 스토어드 프로시저라고 불리며, 줄여서 SP라고 한다.
+ 일련의 쿼리를 마치 하나의 함수처럼 실행하기 위한 쿼리의 집합
+ 특정 작업을 위한 쿼리, 즉 작업들을 정리한 절차
+ 함수와 거의 비슷하지만 차이점이 있다.

### 장점
- 하나의 요청으로 여러 SQL문을 실행 가능 (네트워크 부하를 줄여줌)
- 네트워크 소요 시간을 줄여 성능 개선 가능
- 절차적 기능 구현 (SQL 쿼리는 절차적 기능 제공하지 않지만, SP는 IF, While과 같은 제어문 허용)
- 개발 업무 구분 (App 개발자와 DB개발 조직을 구분 지을 수 있음)-> SP를 수정하려면 DB인력 필요하기 때문에 단점이 될 수도 있음
- 기능 변경이 편리 (특정 기능을 변경할 때 프로시저만 변경하는 식으로)
- 서버 재기동이 필요 없고 SP만 수정하면 관리되는 경우 장점이 됨

### 단점
- 문자나 숫자열 연산에 사용 시 오히려 C, Java보다 성능 저하를 유발할 수 있음
- 유지보수가 어려움 (문서화 해두지 않으면 어디에 사용되는지 파악 어려움, 트리거와 비슷)


## 📌 그래서 차이점은?

+ <span style="color:green">트리거</span>는 이벤트가 발생할 때 자동으로 호출<br>(DDL, DML, 또는 일부 DB 작업(LOGOFF, SHUTDOWN)에 대한 응답)
<br><span style="color:red">프로시저</span>는 필요할 때마다 호출

+ <span style="color:green">트리거</span> 내부에서 프로시저 정의 가능
<br><span style="color:red">프로시저</span> 내부에서 트리거 정의 불가 (트리거는 이벤트 발생 시 자동으로 호출되어야 하므로)

+ <span style="color:green">트리거</span>는 매개 변수 값이나 코드를 반환할 수 없음
<br><span style="color:red">프로시저</span>는 매개 변수 값이나 코드를 반환할 수 있음 (리턴값 없어도 됨, 수행하는 절차가 목적이기 때문)


## Reference!
<br>
트리거

[https://vvshinevv.tistory.com/42](https://vvshinevv.tistory.com/42)

[https://hanhyx.tistory.com/20](https://hanhyx.tistory.com/20)

[https://velog.io/@eeun95/TRIGGER-vs-PROCEDURE](https://velog.io/@eeun95/TRIGGER-vs-PROCEDURE)

프로시저

[https://yuchae.tistory.com/51
](https://yuchae.tistory.com/51)

[https://fomaios.tistory.com/entry/PLSQL-%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80Procedure%EB%9E%80-feat-CRUD](https://fomaios.tistory.com/entry/PLSQL-%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80Procedure%EB%9E%80-feat-CRUD)

[https://graduation.tistory.com/444](https://graduation.tistory.com/444)

[https://velog.io/@minsuk/%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80-%ED%8A%B8%EB%A6%AC%EA%B1%B0-%EC%82%AC%EC%9A%A9%EC%9E%90%EC%A0%95%EC%9D%98%ED%95%A8%EC%88%98-%EC%B0%A8%EC%9D%B4](https://velog.io/@minsuk/%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80-%ED%8A%B8%EB%A6%AC%EA%B1%B0-%EC%82%AC%EC%9A%A9%EC%9E%90%EC%A0%95%EC%9D%98%ED%95%A8%EC%88%98-%EC%B0%A8%EC%9D%B4)