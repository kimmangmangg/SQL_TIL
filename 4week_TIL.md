# 4-4. 날짜 및 시간 데이터 이해하기(2)<br>
### 1️⃣ CURRENT_DATETIME : 현재 DATETIME 출력<br>
```
SELECT
  CURRENT_DATE() AS current_date,
  CURRENT_DATE("Asia/Seoul") AS current_date_asia,
  CURRENT_DATETIME() AS current_datetime,
  CURRENT_DATETIME("Asia/Seoul") AS current_datetime_asia
```
<img width="716" alt="Image" src="https://github.com/user-attachments/assets/a5a83a98-462c-4a7c-976f-63af16b2b572" /><br>
⚠️ CURRENT_DATETIME의 경우, 괄호 안에 타임존을 설정하지 않으면 UTC가 출력되므로 오전 9시간 이전에 실행하면 날짜가 다르게 출력될 수있으니 주의<br><br><br>


### 2️⃣ EXTRACT : DATETIME에서 특정 부분만 추출하고 싶은 경우<br>
일자별 주문, 월별 주문 등 구하고 싶을 때 → 데이트타임에서 일자/월자만 뽑아서 변환해줄 때 사용<br>
```
SELECT
  EXTRACT(DATE FROM DATETIME "2024-05-06 14:00:00") AS date,
  EXTRACT(MONTH FROM DATETIME "2024-05-06 14:00:00") AS month,
  EXTRACT(DAY FROM DATETIME "2024-05-06 14:00:00") AS day
```
<img width="439" alt="Image" src="https://github.com/user-attachments/assets/01c7e68b-0e0f-4ead-8cb2-60d38e7174f0" /><br>
⚠️ DATE는 전체 날짜(년-월-일) 출력, DAY는 일자 출력<br><br>

```
SELECT
  EXTRACT(DATEOFWEEK FROM datetime_col)
```
➡️ 일요일=1 월요일=2 ... 토요일=7로 반환<br><br>

```
SELECT
  DATETIME_TRUNC(datetime_col, HOUR)
```
e.g. 2025-05-05 14:42:13 ➡️ 2025-05-05 14:00:00 <br>
```
SELECT
  DATETIME_TRUNC(datetime_col, YEAR)
```
e.g. 2025-05-05 14:42:13 ➡️ 2025-01-01 00:00:00<br>
✅ EXTRACT와 DATETIME_TRUC 중 상황에 맞게 사용하기~<br><br><br>


### 3️⃣-1️⃣ PARSE_DATETIME : 문자열로 저장된 DATETIME을 DATETIME타입으로 바꾸고 싶은 경우<br>
- DATETIME의 경우 문자열로 저장될 수 있음!
- 문자열에서 알맞은 값을 연도, 월, 일, 시, 분, 초로 파싱해주기
- **파싱하다** : 분석해서 알맞은 것으로 배치/변환한다.

```
SELECT
  PARSE_DATETIME('파싱시키고 싶은 문자열 형태', 'DATETIME문자열')
```
e.g.
```
SELECT
  PARSE_DATETIME('%Y-%m-%d %H:%M:%S', '2025-05-05 12:34:56')
```
➡️ 출력된 값은 알맞게 파싱된 데이트 타입의 데이터로 변환 !<br>
➡️ Format Elements 문서에서 확인해서 사용하기<br><br>


### 3️⃣-2️⃣ FORMAT_DATETIME : DATETIME타입 데이터를 문자열로 바꾸고 싶은 경우<br>
```
SELECT
  FORMAT_DATETIME('%c', DATETIME "2025-05-05 12:34:56") AS formatted;
```
<br>

### 4️⃣ LAST_DAY : 자동으로 마지막 날 연산<br>
```
SELECT
  LAST_DAY(DATETIME "2024-01-03 15:30:00") AS last_day,
  LAST_DAY(DATETIME "2024-01-03 15:30:00", WEEK) AS last_day_week,
  LAST_DAY(DATETIME "2024-01-03 15:30:00", WEEK(SUNDAY)) AS last_day_week_sun,
  LAST_DAY(DATETIME "2024-01-03 15:30:00", WEEK(MONDAY)) AS last_day_week_mon
```
➡️ 인자 없이 출력(last_day)하면, 그 달의 마지막 날 출력<br>
➡️ 인자를 WEEK이나 WEEK(SUNDAY)로 설정하면, 일요일을 기준으로 해당 주 마지막 날(토요일) 출력<br>
➡️ WEEK(MONDAY)로 설정하면, 월요일을 기준으로 해당 주 마지막 날(일요일) 출력<br><br><br>

### 5️⃣ DATE_DIFF : 두 DATETIME의 차이<br>
```
SELECT
  DATE_DIFF(first_datetime, second_datetime, DAY) AS day_diff1,
  DATE_DIFF(second_datetime, first_datetime, DAY) AS day_diff2,
  DATE_DIFF(first_datetime, second_datetime, MONTH) AS month_diff1,
  DATE_DIFF(first_datetime, second_datetime, WEEK) AS week_diff
```
<img width="734" alt="Image" src="https://github.com/user-attachments/assets/4c197a79-46e4-4cd8-8a03-9bd7671ae0fd" /><br>
<img width="562" alt="Image" src="https://github.com/user-attachments/assets/608b988a-f48b-40af-8032-33399b22ea4e" />
### ➕ 서브쿼리 사용하여 변수 지정해서 구하기
<img width="519" alt="Image" src="https://github.com/user-attachments/assets/e44ca21b-93b0-43e2-b0f5-ea0ef4f9d163" /><br>
<img width="559" alt="Image" src="https://github.com/user-attachments/assets/ba9cfd5b-73bc-45e2-8196-e8f2d096f97e" /><br>
➡️ 첫 값이 더 커야 양수가 나옴<br><br><br>


# 4-6.조건문(CASE WHEN, IF)
- 특정 조건이 참일 때 A, 아니면 B를 해라
- 조건에 따라서 다른 값 or 다른 액션을 해라
- 조건문 사용 예시 : 특정 카테고리(저학년/고학년, 평일/주말 등)를 하나로 합치는 전처리<br><br>

### 1️⃣ CASE WHEN : 여러 조건 설정시 유용
```
SELECT
  CASE
  WHEN 조건1 THEN 조건1이 참일 경우의 결과
  WHEN 조건2 THEN 조건2가 참일 경우의 결과
  ELSE 그 외 조건일 경우의 결과
END AS 새로운_칼럼_이름
FROM 테이블
```

**✅ CASE WHEN은 순서가 매우 중요**<br>
e.g. 공격력(attack)이 50이상이면 'strong', 100이상이면 'very strong', 그외는 'weak'으로 분류하라<br>
➡️ 순서대로 실행되기 때문에 CASE WHEN에서 **숫자가 작은 50이상인 경우를 먼저 작성**해주기<br>
```
SELECT
  CASE
  WHEN attack >= 50 THEN 'strong'
  WHEN attack >= 100 THEN 'very strong'
  ELSE 'weak'
END AS attack_level
FROM basic.pokemon
```

### 2️⃣ IF : 단일 조건 설정시 유용
```
SELECT
  IF(조건문, True일 때의 값, False일 때의 값) AS 새로운_칼럼_이름
FROM 테이블
```
<br><br>

# 4-9. BigQuery 공식 문서 확인하는 법
- 프로그래밍 언어, 라이브러리 등은 해당 기술 사용법에 대한 공식 문서를 제공함
- "기술명+documentation"으로 구글링
  e.g. BigQuery Documentation 구글링
  e.g. BigQuery CONCAT(함수) Documentation 구글링
- 어떻게 해야할지 모르겠을 때!
  e.g. i want to change string to int **in BigQuery** 구글링
- RSS Feed 구독하면 빅쿼리에 새로운 글(기능)이 올라올 때 바로 알 수 있음!

<br><br>

> ## 🏆 **학습인증**<br>
![Image](https://github.com/user-attachments/assets/a54e7c1d-9d1b-4f04-a1ef-238d9f7009e0)




