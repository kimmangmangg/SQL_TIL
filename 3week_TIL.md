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
✅ MEANING : SELECT 문이 비어있다<br>

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

