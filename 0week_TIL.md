# **1-1. BigQuery 기초지식<br>**
### **[데이터 저장 형태]<br>**
보통 데이터베이스 테이블에 저장<br>

### **[데이터 저장 장소]<br>**
1. MySQL, Oracle, PostgreSQL, AWS Aurora(클라우드) 데이터베이스 주로 사용 → 회사 by 회사
2. OLTP(OnLine Transaction Processing)이라는 공통점이 있음.<br>

- OLTP?<br>
  - 거래를 하기 위해 사용되는 데이터베이스 (e.g. 음식주문)<br>
  - 보류, 중간 상태가 없음 = 데이터가 무결함.<br>
  - 데이터의 추가(INSERT), 변경(UPDATE) 등이 자주 발생.<br>
  - SQL을 사용하여 데이터 추출 가능.<br>
  - But 분석을 위해 만든게 아니라서 속도가 느리고 편의기능이 좀 떨어짐.<br>
  
### **[SQL(Structured Query Language)]<br>**
데이터베이스에서 데이터를 추출/관리할 때 사용하는 프로그래밍 언어<br>

### **[OLAP와 DW]<br>**
- OLAP(Online Analytical Processing) : OLTP의 속도, 기능에 대해 보완이 된, 분석을 위한 기능이 제공되는 서비스
- DW(Data Warehouse) : 여러 데이터(DB,웹크롤링,csv파일,API결과 등) 들을 한 곳에 모아서 저장하는 창고<br>

### **[BigQuery]<br>**
Google Cloud의 OLAP이자 DW<br>
- 난이도 : SQL을 이용해 데이터 추출 가능<br>
- 속도 : OLTP보다 압도적으로 속도가 빠름 (but 돈이 든다)<br>
- Firebase, Google Analytics4(앱/웹 개발시 많이 사용되는 도구)의 데이터가 자동으로 저장되어 손쉽게 추출 가능<br>
- 사용 기기, 위치, OS버전, 이벤트 행동 등 추출 가능<br>
- 데이터 웨어하우스를 사용하기 위해 서버나 컴퓨터를 띄울 필요 없이 구글에서 서버(인프라)를 관리함<br>
- BigQuery 비용(US기준) : 쿼리비용과 저장비용이 있음<br><br>

 
# **1-2. BigQuery 환경설정<br>**   
<img width="1677" alt="Image" src="https://github.com/user-attachments/assets/05b0bbc6-8318-4136-adff-ad2c9086c58b" /> <br>

### **[BigQuery의 환경 구성 요소]<br>**
1. 프로젝트: 여러 데이터셋으로 이루어짐 (가장 큰 단위)<br>
2. 데이터셋: 다양한 테이블로 이루어짐<br>
3. 테이블: 행, 열로 이루어진 데이터 (엑셀, 스프레드 시트)<br>

### **[테이블 생성]<br>**
<img width="1677" alt="Image" src="https://github.com/user-attachments/assets/45db1a8f-b72f-474c-89ea-4d193a7c3e98" /><br>

### **[쿼리 실행해보기]<br>**
<img width="563" alt="Image" src="https://github.com/user-attachments/assets/e03ed5c6-6245-4bca-8791-f0b7c4573aa3" /><br>
<img width="1269" alt="Image" src="https://github.com/user-attachments/assets/cb877fc9-9689-44fc-b8ae-4aacb7c39a78" /><br>
- 쿼리 안에서는 프로젝트 이름(inflearn-bigquery-454511)을 명시하지 않아도 됨.<br><br>


# **2-1. 데이터 활용 Overview<br>**
### **[데이터활용 과정]<br>**
1️⃣ **문제 정의**: 어떤 일을 해야한다 - MECE<br>
2️⃣ **목적 설정**: 원하는 것을 정한다 - MECE<br>
3️⃣ **데이터 탐색**: 단일/다량 자료 확인 - 조건 필터링, 일부 추출, 데이터 변환, 데이터 요약(집계)<br>
4️⃣ **데이터 결과 검증**: 예상과 실제가 동일한가?<br>
5️⃣ **피드백** or **데이터 활용**<br>

- **3️⃣ 데이터 탐색**과 **4️⃣ 데이터 결과 검증**의 과정에서 **SQL**을 사용함<br>
- **MECE**: 중복이 없고 상호배제적이다. so what? 🔁 why so?<br> → 고객/타겟 정의, 지표 정의(metric) 등<br><br>


# **2-2. 저장된 데이터 확인하기(데이터베이스, 데이터웨어하우스, ERD)<br>**
### **[SQL 쿼리를 작성하기 전]<br>**
- 데이터가 **어떻게 저장**되어 있고, **어떤 데이터**가 저장되어 있고, **컬럼의 의미**는 무엇일까?<br> e.g. 이커머스 회사의 물품 창고, 다이소 → 내가 원하는 물품을 찾기 위해 카테고리(위치) 먼저 확인<br>
- 예시처럼 우리는 DW에 데이터가 어떻게 저장되어 있는지 확인하는 과정을 가져야 !<br>

### **[ERD(Entity Relationship Diagram)]<br>**
- 데이터베이스 구조(데이터 저장 형태)를 한눈에 알아보기 위해 사용.<br>
![Image](https://github.com/user-attachments/assets/98f64c21-3197-4b5f-a61b-e4580e3f5bd8)<br>
- ERD가 없다면, 모든 데이터베이스를 직접 보면서 탐색해야 함.<br> (어떤 테이블/컬럼이 존재하고, row개수, 어떤 컬럼으로 연결되었는지, 컬럼의 값들의 의미를 가지는 지 등..)<br>
- 주요 테이블 부터 정의,정리 !<br> **e.g.** 유저/배송/물건 테이블(결과 데이터), 유저 flow 로그 데이터(과정 데이터), 공공 데이터, 서드파티 데이터(외부 솔루션 데이터)..<br>

### **[포켓몬 데이터와 이커머스 데이터]<br>**
- **어떤 데이터**가 있을까?<br>
  - 포켓몬, 트레이너, 트레이너가 잡은 포켓몬, 트레이너가 도전한 유저 배틀, 트레이너가 도전한 체육관 배틀, NPC, 상점, 상점 별 판매 제품..
  - 상품, 고객, 주문, 장바구니 물건, 웹페이지 접근 수, 웹페이지의 버튼 클릭 수..<br><br>

<img width="1679" alt="Image" src="https://github.com/user-attachments/assets/9e32332a-c139-48f6-a22a-6eb3ce93b7c3" /><br>
![Image](https://github.com/user-attachments/assets/7b4a7364-c4de-4aae-88d1-9de143849288)<br>
- 보통 **_id**가 테이블을 연결할 때 사용되는 칼럼일 확률이 높음 !<br><br>

# **3. 학습인증<br>**
<img width="407" alt="Image" src="https://github.com/user-attachments/assets/5a738af0-ccd8-4fac-98c3-f4c92b71b497" />
