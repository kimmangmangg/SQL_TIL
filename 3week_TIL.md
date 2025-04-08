# **3-4. 오류 디버깅 방법<br>**
오류메세지에서는 문제가 되는 지점을 알려줌 !<br>

### Syntax Error (문법 오류)
- 문법이 지켜지지 않은 경우
- **에러 메세지 번역/해석(구글링, chatGPT, 공식문서 등) ⭢ 해결책 모색**
- 데이터 예시, 쿼리, 오류 메세지를 함께 chatGPT에게 제공해서 물어보는 것 추천
- 밑줄 앞이나 뒤에 오류가 있을 확률이 큼<br><br>

**e.g.1<br>**
```
SELECT

FROM basic.pokemon
```
⛔ ERROR : SELECT list must not be empty at [10:1]<br>
✅ MEANING : SELECT 문이 비어있으면 안 됨<br>

```
SELECT
  col
FROM basic.pokemon
```
<br>

**e.g.2<br>**
```
SELECT
  COUNT(id, kor_name)
FROM basic.pokemon
```
⛔ ERROR : Number of arguments does not match for aggregate function COUNT<br>
✅ MEANING : 카운트 함수는 괄호 안에 하나의 인자만 들어가기 때문에 오류 발생<br>
```
SELECT
  COUNT(id)
FROM basic.pokemon
```
<br>

**e.g.3<br>**
```
SELECT
  type1,
  COUNT(id) AS cnt
FROM basic.pokemon
```
⛔ ERROR : SELECT list expression references column type1 a which is neither grouped nor aggregated<br>
✅ MEANING : 집계함수를 사용하였으니, type1으로 GROUP BY가 있어야 함<br>
```
SELECT
  type1,
  COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
  type1
```
<br>

**e.g.4<br>**
```
SELECT
  type1,
  COUNT(id) AS cnt
FROM basic.pokemon

SELECT
  *
FROM basic.trainer
```
⛔ ERROR :Expected end of input but got keyword SELECT<br>
✅ MEANING : 여러개의 SELECT절 수행시, 하나의 SELECT문 끝에는 세미콜론(;)으로 마무리 지어주기 <br>
```
SELECT
  type1,
  COUNT(id) AS cnt
FROM basic.pokemon;

SELECT
  *
FROM basic.trainer;
```
<br>

**e.g.5<br>**
```
SELECT
  *
FROM basic.trainer LIMIT 10
WHERE
  id = 3
```
⛔ ERROR : Expected end of input but got keyword WHERE at [5:1]<br>
✅ MEANING : LIMIT은 항상 가장 마지막에 가야함<br>
```
SELECT
  *
FROM basic.trainer
WHERE
  id = 3
LIMIT 10
```
<br>

**e.g.6<br>**
```
SELECT
  name
FROM (
SELECT * FROM basic.trainer WHERE id = 3
```
⛔ ERROR : Expected ")" but got end of script at [8:11]<br>
✅ MEANING : 서브쿼리 괄호 닫아주기<br>
```
SELECT
  name
FROM (
SELECT * FROM basic.trainer WHERE id = 3)
```
<br><br>

# **4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)<br>**
- SELECT문에서 데이터를 변환시킬 수 있음
- 데이터 타입에 따라 다양한 함수 존재<br>
### 데이터 타입<br>
: 숫자, 문자, 시간/날짜, 부울, (JSON, ARRAY...) etc<br>
- 사용할 기본 타입들 먼저 학습, 그후에 확장하기<br>
  - **숫자** : 1,2,3, 3.14 ...<br>
  - **문자열** : "나" , "데이터", ...<br>
  - **시간/날짜** : 2024-01-01, 2024-01-01 23:39:10 ...<br>
  - **부울** : 참, 거짓<br>

- 보이는 것과 저장된 것의 데이터 타입이 다를 수 있음
    - 엑셀에서의 빈 값 ⭢ "" or NULL 가능
    - 1 ⭢ 숫자1 or 문자1 가능
    - 2023-12-31 ⭢ DATE 2023-12-31 or 문자 "2023-12-31" 가능
    - TRUE/FALSE ⭢ bool or 문자열 가능
- 이런 경우, 데이터 타입을 서로 변경해줘야 함<br><br>
### CAST와 SAFE_CAST 함수<br>
: 자료 타입 변경 함수<br>
```
SELECT
  CAST(1 AS STRING) # 숫자 1을 문자 1로 바꿈
```
**cf.** <br>
```
SELECT
  CAST("장기하" AS INT64) # 문자열을 숫자로?
```
⛔ 문자열은 숫자로 바꿀 수 없어 오류 발생<br>
```
SELECT
  SAFE_CAST("장기하" AS INT64)
```
✅ SAFE_가 붙은 함수는 변환 실패시 NULL 반환<br><br><br>


# **4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)<br>**
: 따옴표로 묶인 것들이 문자열<br>
### 문자열 대표적인 연산<br>
![Image](https://github.com/user-attachments/assets/785cddad-41ce-4327-b871-749b3d9afcc0)<br><br>
### CONCAT 함수 - 문자열 붙이기
```
SELECT
  CONCAT("안녕","하세요") AS result
```
<img width="545" alt="Image" src="https://github.com/user-attachments/assets/f379682b-d0f1-4ebe-9045-32ab71bfd24f" /><br>
✅ CONCAT 인자로 숫자,STRING 데이터를 직접 넣어준 것이기 때문에 FROM절이 없어도 실행됨 !<br>
### SPLIT 함수 - 문자열 분리하기
```
SELECT
  SPLIT("장기하,와,얼굴들",",") AS result
```
<img width="540" alt="Image" src="https://github.com/user-attachments/assets/1fedcded-5c2f-447f-a172-2a11ad395813" /><br>
✅ SPLIT("문자열 원본","나눌 기준 문자")<br>
✅ 결과값이 배열(ARRAY)로 나옴 - 행이 하나인데, 여러 가지 데이터가 한번에 출력되면 배열임<br>
### REPLACE 함수 - 문자열 수정하기
```
SELECT
  REPLACE("안녕하세요","안녕","실천") AS result
```
<img width="571" alt="Image" src="https://github.com/user-attachments/assets/5a866ded-8b5b-42a5-9b77-8688a82fc73e" /><br>
✅ REPLACE("문자열 원본","찾을 문자","바꿀 문자")<br>
### TRIM 함수 - 문자열 자르기
```
SELECT
  TRIM("장기하와얼굴들","와얼굴들") AS result
```
<img width="528" alt="Image" src="https://github.com/user-attachments/assets/c34d1d61-4c1f-4f24-b22e-49728211832c" /><br>
✅ TRIM("문자열 원본","자르고 싶은 문자")<br>
### UPPER 함수 - 영어 대문자 변환
```
SELECT
  UPPER("abcd") AS result
```
<img width="516" alt="Image" src="https://github.com/user-attachments/assets/6b2aac4e-7cf8-4b3e-bb5f-46ccfc7cff68" /><br><br><br>


# **4-4. 날짜 및 시간 데이터 이해하기(1)<br>**
>## 날짜/시간 데이터 타입 파악 : DATE, DATETIME, TIMESTAMP
- DATE : 2023-12-31 (날짜만)
- DATETIME : 2023-12-31 14:02:19 (날짜 + 시간)
- TIME : 14:02:19 (시간만)<br><br>

>## 날짜/시간 데이터 관련 알면 좋은 내용 : UTC 개념, Millisecond 개념<br>
### 타임존?
- GMT : 경도 0도 지역의 시간 구분선 (한국시간: GMT+9)
- **UTC** : 국제적인 표준 시간, 협정 세계시, GMT와의 차이 미비하긴 함 (한국시간: UTC+9)
- 타임존이 존재한다 = 특정 지역의 표준 시간대
- **TIMESTAMP** : UTC부터 경과한 시간을 나타내는 값, 기준(UTC)으로부터 특정 시점에 도장을 땅 찍어서 그 시점의 시간을 표현한 값
- 타임스탬프는 항상 타임존을 가지고 있음<br><br>
✅ 표현 : 2023-12-31 14:02:19 UTC<br>
### Millisecond, Microsecond
- millisecond(ms) : 천 분의 1초 ,빠른 반응이 필요한 분야에서 사용
- microsecond(us) : 천 분의 1밀리세컨초 (millisecond을 다시 1/1000 한 것)<br><br>
✅ millisecond ⭢ TIMESTAMP ⭢ DATETIME 변환해서 사용<br><br>

>## 날짜/시간 데이터 타입 간 변환<br>
- TIMESTAMP_MILLIS(ms) : 밀리세컨을 TIMESTAMP로 변환
- TIMESTAMP_MICROS(ms+000) : 마이크로세컨을 TIMESTAMP로 변환
- DATETIME(TIMESTAMP~) : TIMESTAMP를 DATETIME으로 변환<br><br>
<img width="692" alt="Image" src="https://github.com/user-attachments/assets/212a75cf-1a5b-4e17-8a0e-2d1b3afbb51a" /><br>
⛔ DATETIME과 TIMESTAMP값이 동일하게 나옴? **타임존**('Asia/Seoul')을 설정하지 않아서 생긴 오류<br>
<img width="904" alt="Image" src="https://github.com/user-attachments/assets/16481d5c-80d2-4a8e-9abb-5e29c57613aa" /><br><br>

### TIMESTAMP와 DATETIME 비교
```
SELECT
  CURRENT_TIMESTAMP() AS TS,
  DATETIME(CURRENT_TIMESTAMP(),'Asia/Seoul') AS DT
```
<img width="518" alt="Image" src="https://github.com/user-attachments/assets/b7f5a661-9fb1-4b8f-a397-76d79c60eb2f" /><br>

- 타임스탬프는 끝에 UTC라고 표시, 데이트타임은 날짜와 시간 사이에 T표시
- 타임스탬프 시간에 +9를 해줘야 한국 시간임<br><br><br>

# 0. 학습인증<br>
![Image](https://github.com/user-attachments/assets/0a4ba50f-9d1e-4f37-b00b-d28959aa3f7f)
