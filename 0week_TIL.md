# **1-1. BigQuery 기초지식**
1. MySQL, Oracle, PostgreSQL 등 데이터베이스 많이 사용 회사바이회사 - OLTP(online transaction processing)이라는 공통점이 있음.


2. OLTP(Online Transaction Processing): 거래를 하기 위해 사용되는 데이터베이스. 데이터가 무결함. 데이터의 추가(INSERT), 변경(UPDATE)등 자주 발생. 분석을 위해 만든게 아니라서 속돌가 느리고 편의기능이 좀 떨어짐
transaction을 위해 만들어진 것.

3. SQL(Structured Query Language) : 데이터베이스에서 데이터를 추출할 때 사용하는 언어. 데이터베이스의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어.

4. OLAP(Online Analytical Processing), DW(Data Warehouse) : OLTP의 속도, 기능에 대한 보완이 된 분석에 적합한 OLAP 등장. DW: 다양한 데이터를 한 곳에 모은 곳

5. BigQuery : Google Cloud의 OLAP이자 DW

6. BigQuery 장점 : SQL을 사용해 쉽게 데이터 추출 가능 / OLAP 도구이므로 속도 빠름(but 돈이 든다)

7. Firebase, Google Analytics4의 데이터 쉽게 추출 가능. 데이터 웨어하우스를 사용하기 위해 서버를 띄울 필요 없이 구글에서 인프라를 관리함

8. BigQuery 비용(US기준) : 쿼리비용) 쿼리에서 처리된 용량만큼 부과 or Slot단위로 요금 부과 / 저장비용) 저렴함

# **1-2. BigQuery 환경설정**   

1. 프로젝트: 다양한 데이터셋으로 이루어짐 (가장 큰 단위)
2. 데이터셋: 다양한 테이블로 이루어짐
3. 테이블: 행, 열로 이루어진 데이터 (엑셀, 스프레드 시트)
**<img width="1180" alt="Image" src="https://github.com/user-attachments/assets/2ec92a14-b160-4df3-b7c6-3ad0951353bd" />**
4. `을 '로 헷갈려서 오류 발생했었음
<img width="1235" alt="Image" src="https://github.com/user-attachments/assets/fe121090-ffcc-424b-a96f-b23c59b018f4" />

# **2-1. 데이터활용 Overview**
**데이터활용과정**
1. 어떤 일을 해야한다
2. 원하는 것을 정한다
3. 데이터 탐색(단일, 다량 자료)
4. 필터링, 추출, 변환, 요약
5. 데이터 결과 검증
6. 피드백, 활용

# **2-2. 저장된 데이터 확인하기(데이터베이스, 데이터웨어하우스, ERD)**
1. SQL 쿼리를 작성하기 전, 데이터가 어떻게 저장되어 있고, 어떤 데이터가 저장되어 있고 컬럼의 의미는 무엇인지..
2. 데이터 추출 전, DW에 데이터가 어떻게 저장되어 있는지.. 확인해야 하자!

3. ERD(Entity Relationship Diagram): 데이터베이스 구조를 한눈에 알아보기 위해 사용.
4. ERD가 없다면, 모든 데이터베이스를 직접 보면서 탐색해야 함. (어떤 테이블과 컬럼이 존재하고, 어떤 컬럼을 사용하여 연결하고, 컬럼의 값들은 어떤 의미를 가지는 지 등..)
5. 포켓몬 데이터 : 포켓몬(상품) / 트레이너(유저)/ 트레이너가 잡은 포켓몬(주문) / 트레이너가 도전한 유저 배틀 / 트레이너가 도전한 체육관 배틀 /  NPC / 상점 / 상점 별 판매 제품

# **학습인증**
