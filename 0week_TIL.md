# **1-1. BigQuery 기초지식**
1. MySQL, Oracle, PostgreSQL 등 데이터베이스 많이 사용 회사바이회사 - OLTP(online transaction processing)이라는 공통점이 있음.


2. OLTP(Online Transaction Processing): 거래를 하기 위해 사용되는 데이터베이스. 데이터가 무결함. 데이터의 추가(INSERT), 변경(UPDATE)등 자주 발생. 분석을 위해 만든게 아니라서 속돌가 느리고 편의기능이 좀 떨어짐
transaction을 위해 만들어진 것.

3. SQL(Structured Query Language) : 데이터베이스에서 데이터를 추출할 때 사용하는 언어. 데이터베이스의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어.

4. OLAP(Online Analytical Processing), DW(Data Warehouse) : OLTP의 속도, 기능에 대한 보완이 된 분석에 적합한 OLAP 등장. DW: 다양한 데이터를 한 곳에 모은 곳

5. BigQuery : Google Cloud의 OLAP이자 DW

6. BigQuery 장점 : SQL을 사용해 쉽게 데이터 추출 가능 / OLAP 도구이므로 속도 빠름(but 돈이 든다)

7. Firebase, Google Analytics4의 데이터 쉽게 추출 가능. 데이터 웨어하우스를 사용하기 위해 서버를 띄울 필요 없이 구글에서 인프라를 관리함

8. BigQuery 비용(US기준) : 쿼리비용) 쿼리에서 처리된 용량만큼 부과 or Slot단위로 요금 부과 / 저장비용) 저렴함

# **1-2. BigQuery 환경설정**   

1. 프로젝트: 다양한 데이터셋으로 이루어짐 (가장 큰 단위)
2. 데이터셋: 다양한 테이블로 이루어짐
3. 테이블: 행, 열로 이루어진 데이터 (엑셀, 스프레드 시트)

   
