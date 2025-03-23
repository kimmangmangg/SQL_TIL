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
3. **AS new_name** : Col1을 new_name으로 바꾸겠다.(별칭 지정)<br> **e.g.** **SELECT** * **FROM** basic.pokemon **WHERE** type1="Fire" ( → pokemon 테이블에서 type1이 Fire인 **모든** 칼럼을 출력해라 )<br>
    - 빅쿼리의 경우에는 1TB에 6달러씩 비용이 발생하므로, 필요한 칼럼만 출력하는 것이 좋음
    - 행이 적으면 괜찮지만, 사실 현업에서는 *을 많이 쓰지는 않음
    - 사실 데이터 확인용으로 *출력하는 것인데, 빅쿼리에서 '미리보기'기능을 사용하면 됨<br><br>
4. **SELECT * EXCEPT** : 컬럼이 많고, 제외할 칼럼이 적게 있을 때 사용<br><br>
5. **JOIN** : 테이블을 하나의 집합처럼 생각했을 때, 두 테이블 공통에 있는 데이터를 불러오고 싶다면<br> → 각 테이블에서 데이터를 추출한 후(SELECT), JOIN으로 연결하면 됨.<br><br>
![Image](https://github.com/user-attachments/assets/2cb386f8-3144-402b-b4fe-eb8c9f191ae1)<br><br>


### **[BigQuery Studio]<br>**


 
# **2-4. SELECT 연습문제<br>**
### **[이이야]<br>**
보통 데이터베이스 테이블에 저장<br>

# **2-5. 집계(Group by + having + sum/count)<br>**
### **[이이야]<br>**
보통 데이터베이스 테이블에 저장<br>
