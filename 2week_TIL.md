# **2-6. 연습문제<br>**
## [ 연습문제1 ]
<img width="1568" alt="Image" src="https://github.com/user-attachments/assets/4a3fcd60-9e2e-4e70-838c-0599c5a7013b" /><br>
- IS NULL ( NULL = NULL x )
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
  WHERE cnt >= 2<br><br>
- having을 쓰는게 더 경제적임
## [ 연습문제7 ]
<img width="1566" alt="Image" src="https://github.com/user-attachments/assets/0bf7b75c-2ac7-497f-94ba-92eebc525f2e" /><br>
- or조건으로 풀 수도 있음
- where (name = "Iris") or (name = "Cynthia") or (name = "Whitney")
## [ 연습문제8 ]
<img width="1568" alt="Image" src="https://github.com/user-attachments/assets/65ff54d6-f087-4278-b10d-f973eb4fec20" /><br>
## [ 연습문제9 ]
<img width="1566" alt="Image" src="https://github.com/user-attachments/assets/421cbb33-94a8-4e74-b9b2-0737bfcb3f82" /><br>
