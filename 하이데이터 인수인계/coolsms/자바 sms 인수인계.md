---
theme: gaia
_class: lead 
paginate: true
backgroundColor: #fff
backgroundImage: url('../hidataBg.jpg')
marp: true
---
# COOLSMS 인수인계
### 작성: 이찬영
---
## 개발 환경 
 - JAVA
 - 자바 Quartz CRON 스케쥴러 라이브러리
 - CoolSms RestFull API
 -  mybatis, mariaDB 
 ---
 ## 프로젝트 구조
```
AlarmApp
    - API       //coolsms api 호출 클래스 
    - DAO      
    - model 
    - schedule   // 스케쥴럴를 통해 실행할 잡 클래스
    - service 
    - App.java   //  메인 함수
    - mybatisConnectionFactory.java  // 디비 연결 정보
```
---
## App.java
 - main()
    - 자바 메인함수 JobDetail(실행할 일), Trigger( 언제 잡을 실행 할지)을 지정한다. 

 - getCRON()
    - 데이터 베이스로부터 알람의 설정정보를 받아온다.
---

## CoolSmsAPI.java
- CoolSmsAPI()
    - API 키 정보를 디비에서 조회하여 API 호출시 사용
- sendMessage()
    - param1: toNumber  // 전화번호 
    - param2: Type    // 전송 방식  SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지), ATA(알림톡)
    - param3: text      // 전송 내용
- getBalance()
    - 잔액조회 API 호출하여 로그를 남긴다.

---
## AlarmSchedule.java 
 - AlarmSchedule()
    - 생성자
 - execute()
    - 전송할 데이터를 가져와 API 를 사용하여 전송한다
    - 전송실패시 잔액을 확인한다.
- getData()
    - 디비로 부터 메세지 정보 조회
---


