# **2-3. 데이터 탐색(SELECT, FROM, WHERE)<br>**
### **[포켓몬으로 SELECT 이해하기]<br>**
-  어떤 포켓몬과 여행을 시작할까?<br>
   - 이름, 공격력/방어력 높은 포켓몬, 타입 등 선택 기준이 있을 것<br>
- SQL쿼리를 짤 때에도 이러한 사고의 흐름을 따라야  함.<br>

### **[SQL 쿼리 구조]<br>**
1. 빅쿼리도 (구글)SQL을 사용.<br><br>
**SELECT<br>** Col1 AS new_name, Col2, Col3 ( → 출력 칼럼 )<br>
**FROM<br>** DataSet.Table ( → 어떤 데이터셋의 어떤 테이블에서 데이터를 확인할지 )<br>
**WHERE<br>** Col1=1 ( → 원하는 조건 )<br><br>
2. 쿼리 실행 순서는 **FROM** > **WHERE** > **SELECT<br><br>**
3. **AS new_name** : Col1을 new_name으로 바꾸겠다.(별칭 지정)<br> **e.g.** SELECT * FROM basic.pokemon WHERE type1="Fire" ( → pokemon 테이블에서 type1이 Fire인 **모든** 칼럼을 출력해라 )<br>
    - 빅쿼리의 경우에는 1TB에 6달러씩 비용이 발생하므로, 필요한 칼럼만 출력하는 것이 좋음
    - 행이 적으면 괜찮지만, 사실 현업에서는 *을 많이 쓰지는 않음
    - 사실 데이터 확인용으로 *출력하는 것인데, 빅쿼리에서 '미리보기'기능을 사용하면 됨<br><br>
4. **SELECT * EXCEPT** : 컬럼이 많고, 제외할 칼럼이 적게 있을 때 사용<br><br>
5. **JOIN** : 테이블을 하나의 집합처럼 생각했을 때, 두 테이블 공통에 있는 데이터를 불러오고 싶다면<br> → 각 테이블에서 데이터를 추출한 후(SELECT), JOIN으로 연결하면 됨.<br><br>
![Image](https://github.com/user-attachments/assets/2cb386f8-3144-402b-b4fe-eb8c9f191ae1)<br>

### **[BigQuery에서 실습]<br>**
- 최종 수정시간 : 데이터 동기화 시간
- 표 만료 : 만료 데이트
- 미리보기 : 데이터 확인 가능
- 나머지 기능은 추가/삭제되는 편<br><br>
<img width="614" alt="Image" src="https://github.com/user-attachments/assets/b1523c96-3257-4bbd-981a-988f027a8c9e" /><br><br>
1. 프로젝트가 단일이라면, 프로젝트 명(inflearn-bigquery-454511) 명시 안해도 됨 (여러 프로젝트 존재시 명시)
2. 프로젝트 id(inflearn-bigquery-454511) 제외하고 작성시 `없어도 괜찮음 → FROM basic.pokemon ⭕ <br>
3. **id AS pokemon_id**: 테이블 칼럼명이 별칭으로 변경됨 → ⚠️주의⚠️ id AS 'pokemon_id' ❌ (cf. 조건문 WHERE type1="Fire" ⭕)<br><br>
<img width="763" alt="Image" src="https://github.com/user-attachments/assets/f4e675db-fcd8-48b9-bcb0-52479eeaa170" /><br><br>
4. **SELECT * EXCEPT(eng_name)** : eng_name칼럼만 제외되어 출력
5. **가독성** 있는 쿼리를 작성하는 것도 중요 → 회사by회사
6. ;(**semi-colon**)은 쿼리가 끝났음을 알려주는 표식
7. 여러 쿼리문 작성시, 돌리고 싶은 쿼리만 **드래그**해서 cmd+Enter하면 해당 쿼리만 출력됨<br><br><br>
 

# **2-4. SELECT 연습문제<br>**
<br>
1️⃣ 어느 테이블의 데이터? (FROM)<br>
2️⃣ 조건문이 있는가? (WHERE)<br>
3️⃣ 어느 칼럼 출력? (SELECT)<br><br>

**[1번 문제]** trainer 테이블에 있는 모든 데이터를 보여주는 SQL 쿼리를 작성해주세요.<br>
- '모든 데이터'가 모든 칼럼? 모든 행? ... 현업에서는 확인해야 함!<br>

<img width="1254" alt="Image" src="https://github.com/user-attachments/assets/0c908887-c173-4dcc-8c39-a2bd3cd0e554" /><br>

**[2번 문제]** trainer 테이블에 있는 tainer의 name을 출력하는 쿼리를 작성해주세요.<br>
<br>
<img width="167" alt="Image" src="https://github.com/user-attachments/assets/c05fb742-6daa-4c60-8a83-bbb4cd83926b" /><br>

**[3번 문제]** trainer 테이블에 있는 트레이너의 name,age를 출력하는 쿼리를 작성해주세요.<br>
<br>
<img width="168" alt="Image" src="https://github.com/user-attachments/assets/0e978de1-7207-42af-8a63-33d85357547c" /><br>

**[4번 문제]** trainer 테이블에서 idrk 3인 트레이너의 name,age,homtown을 출력하는 쿼리를 작성해주세요.<br>
<br>
<img width="166" alt="Image" src="https://github.com/user-attachments/assets/8edfc1b2-c47d-48a2-a209-dde68fa454e5" /><br>

**[5번 문제]** pokemon 테이블에서  "피카츄"의 공격력과 체력을 확인할 수 있는 쿼리를 작성해주세요.<br>
- 공격력과 체력을 나타내는 칼럼이 무엇일지 데이터를 둘러보며 확인해야 함.<br>

<img width="183" alt="Image" src="https://github.com/user-attachments/assets/61f79fe0-ef27-4c1a-af26-3e0c1d5fef80" /><br><br><br>


# **2-5. 요약, 집계, 그룹화(DISTINCT,GROUP BY,HAVING,SUM,COUNT)<br>**
### **[집계와 그룹화]<br>**
- 집계하다 : 모아서 즉, 그룹화해서 계산하다.<br>
- 계산 : 더하기, 빼기, 최댓값, 최솟값, 평균값, 개수<br>


### **[GROUP BY]<br>**
- 특정 칼럼을 기준으로 같은 값끼리 모아, 다른 칼럼의 값들은 집계(합,평균,max,min 등)한다.<br><br>
**SELECT<br>** *집계할 컬럼1*, 집계 함수(COUNT/MAX/MIN etc.)<br>
**FROM<br>** DataSet.Table<br>
**GROUP BY<br>** *집계할 칼럼1*<br><br>

   [예시]<br>
   **SELECT<br>** *type1*, AVG(attack) AS avg_attack,COUNT(id) AS count<br>
   **FROM<br>** basic.potemon<br>
   **GROUP BY<br>** *type1*<br><br>

- GROUP BY해준 *집계할 칼럼*은 반드시 **SELECT절**에 명시해야 함.<br>

### **[DISTINCT]<br>**
- 여러 값 중에 Unique한 값만 보고 싶은 경우 사용<br>
**e.g.** COUNT(DISTINCT 컬럼1) : 칼럼1의 고윳값만 계사나해서 개수를 세어라.<br>
- 중복을 제거할 때 사용되는데, GROUP BY도 중복 제거 효과 있기 때문에 어떤 함수를 사용할지는 상황에 맞춰서!<br><br>
![Image](https://github.com/user-attachments/assets/37021e5e-763c-41c3-9ca0-67208d0a8cfa)<br><br>
- **view 수?** COUNT(user_id)<br>
- **view한 유저의 수?** COUNT(**DISTINCT** user_id)<br>

### **[GROUP BY 연습문제]<br>**
**Q1. pokemon 테이블에 있는 포켓몬 수를 구하는 쿼리를 작성해주세요.<br>**
<br>
<img width="228" alt="Image" src="https://github.com/user-attachments/assets/715da8e0-ec23-4532-994c-ecff8310d238" /><br>
<img width="311" alt="Image" src="https://github.com/user-attachments/assets/4c99001c-3979-4c5e-821a-dbf8268cf445" /><br>
- NULL값이 없어서 id로 COUNT한 값과 *로 COUNT한 값이 동일하게 나옴
- 비어있는 값이 있을 때는 id를 사용하는 것이 더 명시적<br>

**Q2. 포켓몬의 수가 세대별로 어라나 있는지 알 수 있는 쿼리를 작성해주세요.<br>**
<br>
<img width="169" alt="Image" src="https://github.com/user-attachments/assets/aea5eedc-4e8a-40cd-9796-1a372697caa2" /><br>
<img width="310" alt="Image" src="https://github.com/user-attachments/assets/14fa06c3-f2e4-4e8e-bd4f-f66f71b513dc" /><br>


### **[WHERE과 HAVING]<br>**
- WHERE : 테이블에 바로 조건을 설정할 때
- HAVING : GROUP BY한 이후! 조건을 설정할 때<br><br>

   [예시]<br>
   **SELECT<br>** Col1,Col2,COUNT(Col1) AS *col1_cnt*<br>
   **FROM<br>** table<br>
   **GROUP BY<br>** Col1,Col2<br>
   **HAVING<br>** *col1_cnt*>3<br><br>

- *col1_cnt*는 그룹바이 이후에 생겨난 칼럼
- 서브쿼리 개념을 이용해서도 나타낼 수 있음
- WHERE과 HAVING 같이도 사용 가능<br>

### **[서브쿼리]<br>**
- SELECT문 안에 존재하는 SELECT쿼리
- FROM절에 SELECT문을 넣을 수 있음 (괄호로 묶어서 사용)
- 서브쿼리 하나가 일종의 테이블 역할을 하기 때문에
- 서브쿼리 작성 후 서브쿼리 바깥에서 WHERE조건 설정하는 것과 서브쿼리에서 HAVING으로 조건 설정하는 것은 같음.<br>

### **[ORDER BY]<br>**
- **SELECT<br>** Col1<br>
**FROM<br>** table<br>
**ODER BY<br>** Col1 DESC/ASC<br><br>
- 쿼리의 가장 마지막에서 내림차순(DESC), 오름차순(ASC - 디폴트) 설정
- 중간에 들어가면 연산량이 많아져서 계산 속도 느려짐<br>

### **[LIMIT]<br>**
- 결과 출력시 ROW 수 제한할 때 사용
- 쿼리의 가장 마지막에 사용<br>

### **[GROUP BY 연습문제]<br>**
**Q3. 포켓몬 수를 타입 별로 집계하고, 포켓몬 수가 10이상인 타입만 남기는 쿼리를 작성해주세요.(포켓몬 수가 많은 순으로 정렬)<br>**

<img width="412" alt="Image" src="https://github.com/user-attachments/assets/ffa9caf2-a841-4f83-bb98-ce20538611f6" /><br><br><br>

# **3. 학습 인증<br>**
![Image](https://github.com/user-attachments/assets/7047ea8a-662f-4aec-925d-087278cf6934)
