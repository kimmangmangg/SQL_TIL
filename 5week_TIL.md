# **JOIN 이해하기**<br>
: 공통된 데이터를 통해 두 개 이상의 테이블을 연결하는 것<br><br>

- 연결할 수 있는 key 찾기
- key 값을 기준으로 테이블을 붙여나감
- 컬럼이 추가되는 경우가 대부분
- 보통 id 값이 key로 많이 사용되고, 특정 범위로 JOIN가능
- 테이블 구조를 먼저 파악하는 것이 JOIN을 잘 할 수 있는 팁!
- 개발자 입장에서는 데이터 정규화 때문에 중복을 최소화하기 위해 개별 테이블로 나눠서 저장하는 것이 일반적
- 분석하는 과정에서 필요에 따라 JOIN하여 데이터를 사용
- 최근에는 데이터 웨어하우스에서 JOIN 등 필요한 연산을 해서 데이터 마트를 구축하여 사용하는 경우도 많음<br><br>


<img width="819" alt="Image" src="https://github.com/user-attachments/assets/7cbe2f38-1fc4-4152-b04c-fe23b0606a36" /><br>

### **LEFT(OUTER) JOIN**
: 왼쪽 테이블 기준으로(=그대로 두고) 연결 ➡️ 제일 기준이 되는 방법!<br>

### **RIGHT(OUTER) JOIN**
: 오른쪽 테이블 기준으로(=그대로 두고) 연결 ➡️ 사실상 테이블 순서를 바꾸면, left join과 동일한 결과 출력가능<br>

### **INNER JOIN**
: 두 테이블의 공통 요소만 연결 ➡️ 교집합 개념!<br>

### **FULL(OUTER) JOIN**
: 양쪽 기준으로 연결 / 양쪽 공통된 요소만 연결하는 것 x ➡️ 모든 Key 값의 모든 행 출력<br>

### **CROSS JOIN**
: 두 테이블 각각의 요소 곱해서 연결 ➡️ 데이터가 엄청 많아질 수 있음 <br><br>

<img width="773" alt="Image" src="https://github.com/user-attachments/assets/9602c98c-fc7c-4186-b4db-9b77d4a92d21" /><br><br>



### **✅ SQL 쿼리로 작성하기**
```
SELECT
  A.col1,
  A.col2,
  B.col11,
  B.col12
FROM table1 AS A
LEFT JOIN table2 AS B
ON A.key=B.key
```
- FROM절에서 조인할 두 테이블 각각 별칭 정의
- ON : 조인키 입력 ➡️ 여기서는 A와 B의 key값이 동일한 것만 가져오겠다는 의미
- 결국 SELECT - FROM - 조인종류 - ON 구조<br>

<img width="742" alt="Image" src="https://github.com/user-attachments/assets/b1164c43-7584-4ca7-88a9-64eb9f816a39" /><br>

- CROSS JOIN은 key값과 상관없이 모든 곱을 출력하므로 ON이 필요없음
- 조인을 한 테이블을 기준으로 다시 조인을 걸 수 있음.<br><br>

**e.g.**
```
SELECT
  tp.*,
  t.*,
  p.*

FROM basic.trainer_pokemon AS tp
LEFT JOIN basic.trainer AS t
ON tp.trainer_id=t.id

LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id=p.id
```
<br>

### **✅ JOIN 공부시 헷갈리는 내용**
**1. 여러 JOIN 중 어떤 JOIN을 사용해야하는지**<br>
   : 작업 목적에 따라 선택하기 ➡️ 정 모르겠으면, 일단 left로 시작해보기<br><br>
**2. 어떤 테이블을 왼쪽에 두고, 어떤 테이블을 오른쪽에 두어야 하는지**<br>
   : 기준이 되는 테이블을 왼쪽에 두기 ➡️ 기준값이 존재하고, 데이터 요소들이 빠짐없이 존재하는 테이블<br>
   **e.g.** <br> 
   주문한 유저의 ~를 알고 싶음 : 주문은 무조건 있어야 하니까, Order테이블을 기준으로 User테이블을 left조인<br>
   모든 유저의 주문의 ~를 알고 싶음 : User테이블을 기준으로 Order테이블을 left조인<br><br>
**3. 여러 테이블을 연결할 수 있는지**<br>
   : 조인의 개수 한계는 없지만 너무 많이 조인하는 것은 비추 ➡️ 5개 이상 조인해야할 것 같으면 3개정도씩 끊어서 중간테이블 만들어주기<br><br>
**4. 칼럼은 모두 다 선택해야 하는지**<br>
: 데이터를 추출해서 무엇을 하고자 하는지에 따라 다르지만 사용하지 않을 칼럼은 선택하지 않는 것이 좋음<br><br>
**5. NULL값?** <br>
: 그냥 값이 없다. 알 수 없다. 0이나 공백과는 다름. ➡️ join시 연결할 값이 없는 경우에 나타남<br><br>

> ## **✏️ 학습인증**<br>
<img width="834" alt="Image" src="https://github.com/user-attachments/assets/31165c29-b8d4-44c6-9e34-9ea94c4163e9" />
