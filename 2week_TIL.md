# **2-6. 연습문제<br>**
## [ 연습문제1 ]
<img width="1568" alt="Image" src="https://github.com/user-attachments/assets/4a3fcd60-9e2e-4e70-838c-0599c5a7013b" /><br>
- IS (NOT) NULL ( NULL = NULL x )
## [ 연습문제2 ]
<img width="1569" alt="Image" src="https://github.com/user-attachments/assets/980977d8-1545-46c1-ac51-570a799fde71" /><br>
## [ 연습문제3 ]
<img width="1567" alt="Image" src="https://github.com/user-attachments/assets/9c2f04dc-9678-4f2f-a7a5-664bd3b5cd35" /><br>
- id 칼럼 자체가 중복 없게 설계한 칼럼이기 때문에, 꼭 COUNT(DISTINCT id)로 하지 않아도 됨
- daily active user에서 보통 COUNT(DISTINCT user_id) 하루에 몇 명의 유니크한 유저가 들어왔는지 계산
## [ 연습문제4 ]
<img width="1565" alt="Image" src="https://github.com/user-attachments/assets/2a4e0861-4804-41c6-afa6-8c8a18137aa3" /><br>
- group by 1 : select 하는 칼럼 중 첫 번째 칼럼을 기준으로 그룹바이 해라
- 집계함수가 이미 들어가 있는 칼럼의 경우에는 사용 불가
- order by 1 : select 하는 칼럼 중 첫 번째 칼럼을 기준으로 오더바이 해라
## [ 연습문제5 ]
<img width="1566" alt="Image" src="https://github.com/user-attachments/assets/01f2a308-aa7e-4002-afb8-1c661e639616" /><br>
- 서브쿼리로도 풀 수 있음.<br>
- SELECT *<br>
  FROM **(SELECT name, count(name) as trainer_cnt FROM basic.trainer GROUP BY name)**<br>
  WHERE cnt >= 2<br>
- having을 쓰는게 더 경제적임
## [ 연습문제7 ]
<img width="1566" alt="Image" src="https://github.com/user-attachments/assets/0bf7b75c-2ac7-497f-94ba-92eebc525f2e" /><br>
- or조건으로 풀 수도 있음
- where (name = "Iris") or (name = "Cynthia") or (name = "Whitney")
## [ 연습문제8 ]
<img width="1568" alt="Image" src="https://github.com/user-attachments/assets/65ff54d6-f087-4278-b10d-f973eb4fec20" /><br>
## [ 연습문제9 ]
<img width="1566" alt="Image" src="https://github.com/user-attachments/assets/421cbb33-94a8-4e74-b9b2-0737bfcb3f82" /><br>
## [ 연습문제10 ]
<img width="1569" alt="Image" src="https://github.com/user-attachments/assets/35009fd5-e203-4c65-b07b-4eb496cde1a5" /><br>
## [ 연습문제11 ]
<img width="1566" alt="Image" src="https://github.com/user-attachments/assets/3c96b040-b639-4542-83f2-a36d7af17e97" /><br>
- limit 1 설정해주면 가장 많은 것 하나만 출력
## [ 연습문제12 ]
<img width="1568" alt="Image" src="https://github.com/user-attachments/assets/d5d9c37d-1d09-4061-8b0e-3ca9d3b45abf" /><br>
## [ 연습문제13 ]
<img width="1569" alt="Image" src="https://github.com/user-attachments/assets/5f7f8ae8-b307-4e31-b98d-d88cdae97cd2" /><br>
## [ 연습문제14 ]
<img width="1567" alt="Image" src="https://github.com/user-attachments/assets/6cd3e3bf-3bd2-41cb-a49f-a13a61460e65" /><br>
## [ 연습문제15 ]
<img width="1568" alt="Image" src="https://github.com/user-attachments/assets/3f790007-30df-42ae-9c34-d3b344ec9a18" /><br>
- 익숙하지 않은 칼럼일 경우, distinct 붙여서 해보고 결과가 동일한지 확인해보기
## [ 연습문제16 ]
<img width="1565" alt="Image" src="https://github.com/user-attachments/assets/670788bf-3fb9-4717-9ad2-4df2ffb6e356" /><br>
## [ 연습문제17 ]
<img width="1568" alt="Image" src="https://github.com/user-attachments/assets/1a7accae-2731-4b1e-9676-56b04ea06397" /><br>
- 하나씩 단계적으로 풀기 !!<br><br><br><br>

# **2-8. 새로운 집계함수<br>**
## [GROUP BY ALL]
- select로 출력되는 칼럼을 모두 추론해서 알아서 그룹바이 해줌
- 즉, GROUP BY 뒤에 여러개의 칼럼명을 명시하지 않아도 됨<br><br><br><br>

# **3-1. SQL 잘 작성하기! 인트로<br>**
- SQL 쿼리 작성하는 흐름
- 쿼리 작성 템플릿과 생산성 도구
- 오류를 디버깅(해결)하는 방법<br><br><br><br>

# **3-2. SQL 쿼리 작성하는 흐름<br>**
1️⃣ 지표 고민 : 어떤 문제를 해결하기 위해 데이터가 필요한가?<br>
2️⃣ 지표 구체화 : 추상적이지 않고(이름 구체적으로 작성), 구체적인 지표 명시(분자, 분모 표시)<br>
3️⃣ 지표 탐색 : 유사한 문제를 해결한 케이스가 있는지 확인 (해당 쿼리 리뷰, 구글링, ai...)<br>
4️⃣ 쿼리 작성 : 데이터가 있는 테이블 찾기 → 1개 or 2개 이상: JOIN으로 연결해서 찾기<br>
5️⃣ 데이터 정합성 확인 :  예상한 결과와 동일한지 확인<br>
6️⃣ 쿼리 가독성 : 나중을 위해 !<br>
7️⃣ 쿼리 저장 : 쿼리는 재사용되므로 문서로 저장<br>
- 실제 회사에서는 지표 고민, 정합성 확인, 가독성 확보하기 부분이 중요함<br><br><br><br>

# **3-3. 쿼리 작성 템플릿과 생산성 도구<br>**
## [템플릿]
- 쿼리 작성 목표, 확인할 지표 : 정의 작성하기
- 쿼리 계산 방법 : 집계, 칼럼 그대로 쓰는가 ..등
- 데이터의 기간 : 회사에서는 항상 기간을 따짐 !
- 사용할 테이블
- join KEY : 두 개 이상의 테이블 사용할 때
- 데이터 특징 : 어떤 칼럼은 어떤 값을 가지고 있고, 특징이 있다..
- SELECT<br><br>FROM<br>WHERE<br>

## [생산성 도구 - espanso]
- 핵심 로직 : 특정 단어가 감지되면 정의된 것으로 바꾼다!<br>
![Image](https://github.com/user-attachments/assets/03e2b9ff-020d-4be8-8db7-2c514348f075)<br>
- matches에 수정해서 템플릿 등록하기<br><br><br>

# **0. 학습 인증<br>**
![Image](https://github.com/user-attachments/assets/933366e4-b6c4-4101-bd60-119f7d17de3d)
![Image](https://github.com/user-attachments/assets/f7a78aa1-82f5-43c9-9da9-90c2cf135482)








