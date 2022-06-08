# _SQL_Grammer_
&nbsp;
## ※DDL, DML, DCL에 관련해서

| 용어 | 종류 |
| ------ | ------ |
| DDL | CREATE / ALTER / DROP |
| DML | SELECT / INSERT / UPDATE / DELETE |
| DCL | GRANT / REVOKE |

- DDL : CREATE / ALTER / DROP
- DML : SELECT / INSERT / UPDATE / DELETE
- DCL : GRANT / REVOKE

&nbsp;

## ※CDB와 XEPDB는?
```sh






```
&nbsp;
&nbsp;

## ▶Oracle에서는 문자열을 '' 으로 표시한다. (""아님!)


&nbsp;
&nbsp;

    ★AS 명칭 쓰기 ▶AS 명칭을 쓸때에는 ""으로 묶는다. 
    SELECT SUM(price) 총계  
    SEELCT SUM(price) "총계"  
    SEELCT SUM(price) AS 총계
    SEELCT SUM(price) AS "총계"  
    SEELCT SUM(price) AS "판매 총계" ▶ 별칭이름에 공백이 포함될 경우에는 반드시 "" 사용  

----------------
&nbsp;

## ※DISTINCT 사용법

    SELECT DISTINCT(컬럼명) FROM 테이블명  
    
    ** COUNT를 같이 사용할때**  
    SELECT **COUNT(DISTINCT 컬럼명)** FROM 테이블명

----------------
&nbsp;

## ※CHARACTER 형식



```sh
1) CHAR : CHAR(50)처럼 쓰며 50의 공간을 쓰지않아도 50개의 공간을 차지하고있다. 
          따라서 고정길이일때 사용하는것이 좋다. (가변길이 적함X)
2) VARCHAR2 : VARCHAR2(50) 처럼 쓰며 괄호안에 숫자는 최대길이의 숫자를 지정해주면 된다. (가변길이 적합O)
3) NCHAR : ???
```

&nbsp;

## ※DATE, TIMESTAMP 형식
> DATE : '2013-02-15' 형식  
> TIMESTAP : 'DATE형식 + 시분초까지'

&nbsp;
&nbsp;
## ※OR, AND, BETWEEN, IN
> IN을 쓰는것이 속도에 더 좋다.
#### EX) 조회수가 0, 1, 2인 게시글을 조회하시오
&nbsp;
WHERE 조회수 = 0 OR 조회수 = 1 .... ▶이렇게 하면  범주가 커지게되면 힘들어질수도있다.

따라서 0~2까지로 범위를 본다면  
WHERER 0<=조회수 AND 조회수 <=2;  
WHERE 조회수 BETWEEN 0 AND 2;  
> ★주로 BETWEEN을 많이 쓴다.

&nbsp;
#### ♠EX) 조회수가 0, 2, 7인 게시글을 조회하시오

WHERER 조회수 == 0 OR .... ▶ 비효휼적.   
> 따라서 IN을 쓴다. : WHERE 조회수 IN(0, 2, 7);

&nbsp;
NOT을 쓸려면 WHERE 조회수 NOT IN(0, 2, 7) : 0, 2, 7만 빼고.
-.> IN절 안에 SELECT절이 추가로 들어갈 수 있다. 

&nbsp;
&nbsp;
## ※LIKE, % == 문자열 패턴을 비교할때 쓰는 연산자    
> _은 한문자 / %는 모든문자. 

##### ♠EX) *회원 중에서 '박'씨 성을 조회하시오.
WHERE 회원이름 LIKE '박%';  
> ★--회원이름 = '박%' : 이렇게 하면 진짜 박%를 찾게된다. 

&nbsp;
&nbsp;

## ※ALL_TAB_COMMENTS
> all_tab_comments : 테이블에 관련된 정보를 한눈에 볼 수 있다.
all_tables작성방법

> comment를 달았기때문에 정보를 참고할 수 있다.
FROM all_col_comments WHERE comments LIKE ~~쓰면 된다.   

**정규식도 참고해보면 좋다. ▶ 정규식은 SQL_RULE편에 있다. 

&nbsp;
&nbsp;
## ※정규식
```sh






```
&nbsp;
&nbsp;

## ※문자열 함수

### ◎SUBSTR(문자열, 시작위치, 길이)
    SELECT SUBSTR('HELLO', 1, 3) FROM 테이블
    SUBSTRB('HELLO', 3) -> Byte단위로 자른다(??)

#### ♠EX) 모든학생의 이름과 출생 월만을 조회하시오

SELECT NAME, SUBSTR(BIRTHDAY, 6, 2) FROM MEMBER; -- 6번째글자부터 2글자만 SUBSTRING해주세요.  
&nbsp;
#### ♠EX) 회원중에서 전화번호가 011로 시작하는 회원의 정보 출력
WHERE SUBSTR(PHONE, 1, 3) = '011'; -> 함수를 쓰는것이 속도문제에서 걸린다.  
WHERE PHONE LIKE '011%' -> 이렇게 하는것이 더 바람직하다.  
> LIKE가 먼저다 라는 생각을 항상 가지고 있으면 좋다.
&nbsp;
#### ♠EX) 회원중에서 폰번호가 없고 생년월일이 7, 8, 9월인 회원정보 출력 
WHERE PHONE IS NULL AND SUBSTR(BIRTHDAY, 6, 2) IN (7, 8, 9);  
WHERE PHONE IS NULL AND SUBSTR(BIRTHDAY, 6, 2) IN ('07', '08', '09');

&nbsp;
### ◎문자열 덧셈 함수
> CONCAT('홍', '길동')
    
&nbsp;
&nbsp;
**<<문자열 더하기 연산자는 무조건 || 이다>>**
    
    select 1 + '2'하면   
    12가 나올것으로 예상하지만, oracle에서는 4가 나온다.
    oracle에서는 +연산자는 무조건 숫자에서만 이뤄지기 때문이다.  
    
    3 || '4' -> 연산자로 쓰는것이 성능이 더 빠르다. 
    

#### ♠EX)모든 회원의 이름을 조회하시오(단, 이름은 ID를 붙여서 나타내시오)
select name || ( || ID || )  
정답: select name || '(' || ID || ')'

&nbsp;
### ◎TRIM 함수 : 빈공백을 없애주는 함수
    LTRIM -> 왼쪽공백만  
    RTRIM  
    TRIM -> 양쪽의 빈공백을 없애준다  

&nbsp;
### ◎ 모두 대소문자로 변경하기
    LOWER('AFJDFKDJKF  
    UPPER

#### ♠EX) 회원의 아이디가 'NEWR'인 사람을 조회하시오(대소문자 상관없이)  
SELECT * FROM MEMBER WHERE UPPER(NAME) = 'jjj';  

#### ♠EX) 이름과 생년월일에서 -을 뺀것을 출력하시오  
SELECT NAME, REPLACE(BIRTHDAY, '-', '') FROM MEMBER;   

&nbsp;
### ◎ LPAD, RPAD
> 문자열 패딩함수

    select LPAD('HELLO', 5) from dual -- 패딩영역이 없기 때문에 문자가 출력되지 않는다.   
    select LPAD('HELLO', 10, '0') from dual -- 나머지 5개가 0으로 채워진다. --00000HELLO : 오른쪽 정렬  
    select RPAD('HELLO', 10, '0') from dual --HELLO00000  
    
#### ♠EX) 이름을 조회하시오(단, 이름의 길이가 3글자가 안되는 경우에는 이름 오른쪽을 '_'로 채우시오
select lpad(이름, 3, '_') from table;  
▶근데 3이라는게 한글일경우 길이가 적용되지 않는다.   

> ★따라서 한글이나, 영문이냐에 따라 padding함수를 잘 활용해야한다. 

&nbsp;
### ◎  INITCAP(문자열) 
> 첫글자를 대문자로 바꾸는 함수
select  initcap('the....') -- The  
select initcap('the camp') -- The Camp (모든 띄어쓰기마다 대문자가 씌워진다.)  
select initcap('the im하이mp c오케mp') -- The Im하이Mp C오케Mp (모든 한글 다음에도 대문자로 표현된다)  

&nbsp;
### ◎  INSTR(문자열, 검색문자열, 위치, 찾을 수)
> 문자열 검색함수  
select instr('all we need' 'all') -- all이 나온 문자열 시작번호를 알려준다. --1  
select instr('all we need' 'we') -- 5  
select instr('all we need' 'all', 1) -> 1번째로 나온 숫자 뭐 이런게 아니라 저건 문자열 index번호이다.  
따라서 index 1 뒤에서부터 count해서 그다음 all이 어디나오냐 약간 이런거다.   
select instr('all we need' 'all', 1, 2) -> index 1부터 찾되 2번재 나온 문자부터 알려달라 == 두번째 all의 시작위치를 알 수 있다. 

#### ♠EX) 전화번호에서 두 번째 대시문자가 존재하는 위치를 출력하시오
select instr(phone, '-', 1, 2)

#### ♠EX) 전화번호에서 첫 번째 -문자와 두 번재 - 문자 사이의 간격 출력
select instr(phone, '-', 1, 2) - instr(phone, '-')  
**정답:** instr(phone, '-', 1, 2) - instr(phone, '-') -1해야 간격이 출력된다. **index끼리 뺀것이기 때문에**

#### ♠EX) 전화번호에서 첫번째와 두번재 사이의 국번을 출력하시오 
substr(phone, 5, 4)  
  
**두번째 숫자가 3자리일수도, 4자리일수도 있기 때문에**  
substr(phone, 5, instr(phone, '-', 1, 2) - instr(phone, '-') -1) 

&nbsp;
### ◎  LENGTH(문자열) 
> 문자열 길이를 얻는 함수

#### ♠EX) 회원의 전화번호에서 -을 없앤 전화번호의 길이를 구하시오.
select length(replace(phone, '-', '')) from member;

&nbsp;
&nbsp;

## ※ROUWNUM
> ROWNUM은 옆에 붙는 숫자이다.
SELECT ROWNUM, NOTICE.*  
FROM NOTICE; -- ROWNUM이 붙어서 나온다. 

    회원목록에서 상위 5명만 조회하시오.  
    WHERE ROWNUM BETWEEN 1 AND 5  
    WHERE ROWNUM BETWEEN 6 AND 10; -- 아무것도 안나옴 ( 2부터 해도 안나온다.)

> ROWNUM은 SELECT 문장이 실행될때 만들어진다.  
따라서 ROWNUM > 5 이렇게 하면 처음에 만들어진 ROWNUM은 항상 1이기 때문에 조건에 맞지 않는다. 

따라서  
SELECT *  
FROM (SELECT ROWNUM NUM, MEMER.* FROM MEMBER)-- ROWNUM은 미리 속괄호에서 붙여준다.  
WHERE NUM BETWEEN 1 AND 5  
▶괄호가 먼저 실행된다.
&nbsp;
> SELECT NOTICE.ID FROM NOTICE; 이렇게 쓰는걸
NOTICE.* 이렇게 쓸 수 있는 것이다. 

&nbsp;
> SELECT * FROM (SELECT ROWNUM, NOTICE.* FROM NOTICE)  
WHERE ROWNUM BETWEEN 6 AND 10;  
-- 실행 X. 왜냐면 ROWNUM이라는게 중복이 되서 괄호 위에 ROWNUM이랑 중복된다.  
따라서 명칭을 붙여줘야한다. 

&nbsp;

    명칭을 붙여서 쓴 최종본
    SELECT * FROM (SELECT ROWNUM NUM, NOTICE.* FROM NOTICE)
    WHERE NUM BETWEEN 6 AND 10;
&nbsp;
&nbsp;
    
## ※숫자함수


1) ABS : 절대값을 구하는 함수
SELECT ABS(35), ABS(-35) FROM DUAL; -- 절댓값 함수

2) SIGN : 음수/양수를 알려주는 함수
SELECT SIGN(35), SIGN(0) FROM DUAL -- 결과값 = 양수:1 음수:-1 영:0

3) ROUND(N, I) : 숫자 반올림 값을 알려주는 함수
SELECT ROUND(34.5678) FROM DUAL -- 결과값 = 35. 
ROUND(34.5678, 2) = 소숫점 둘째자리까지 보여달라(반올림해서) -- 결과값 = 34.57

4) TRUNCATE(값, n) : 버림 - 자릿수 지정
TRUNCATE(8.765, 2) = 8.76

5) CEIL(값, n) : 올림
CEIL(8.765) = 9

6) FLOOR(값, n) : 버림
FLOOR(8.765) = 8

7) MOD(N1, N2) :  숫자의 나머지 값을 반환하는 함수
TRUNC(17/5) -- 결과값=3
MOD(17, 5) -- 결과값=2

8) POWER(N1, N2) / SQRT(N): 숫자의 제곱근을 구하는 함수, 제곱근을 구하는 함수
POWER(5, 2) -- 25
SQRT(25) -- 5
> 값의 n제곱근 구하기 = 값의 1/n제곱을 구하기 = POWER(값, 1/n)

&nbsp;
&nbsp;
## ※날짜함수

1) 현재 시간을 얻는 함수  
SYSDATE, CURRENT_DATE,  
SYSTIMESTAMP, CURRENT_TIMESTAMP

2) 세션 시간과 포맷변경  
(ALTER SESSION SET TIME_ZON = '-1:0' 이건 시간대를 변경하는듯..?)  
ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH24:MI:SS';  
▶SYSDATE, CURRENT_DATE 의 양식을 바꿔준다.

3) 날짜 추출함수 - EXTRACT  
SELECT EXTRAC(YEAR FROM SYSDATE) FROM DUAL;  

4) NEXT_DAY : 다음날을 알려주는 함수  
SELECT NEXT_DAY(SYSDATE, '토') FROM DUAL; -- 토요일이 언제냐. ( 토요일도 가능.)  
SELECT NEXT_DAY(SYSDATE, 7) FROM DUAL;  

6) LAST_DAY : 달의 마지막일을 알고싶을때  
SELECT LAST_DAY(SYSDATE) FROM DUAL; -> 하면 2월의 마지막날이 나온다.  
SELECT LAST_DAY(ADD_MONTHS(SYSDATE, 2)) FROM DUAL; -> 4월의 마지막날이 나온다.  

7) 날짜에서도 ROUND랑 TRUNC가 사용된다.

#### ♠EX) BRTHDAY의 YEAR만 뽑아보기
SELECT EXTRACT(YEAR FROM MEMBER.BIRTHDAY)  
FROM MEMBER;  
> BIRTHDAY는 지금 VARCHAR 형식이여서 추출이 안된다. 따라서 DATE형식으로 바꿔줘야 인식이된다.   
EXTRACT(YEAR FROM TO_DATE(BIRTHDAY,'YYYY-MM-DD')) 


&nbsp;
#### ♠EX)  가입한 회원중에 2, 3, 11월에 태어난 사람의 이름과 생일 출력
SELECT NAME, BIRTHDAY  
FROM MEMBER  
WHERE EXTRACT(MONTH FROM TO_DATE(BIRTHDAY,'YYYY-MM-DD')) IN (2, 3, 11, 12); 
> 'YYYY-MM-DD' 이건 VARCHAR에 들어간 날짜형식대로 넣어줘야한다.

--과장님 답변
SELECT NAME  
      ,BIRTHDAY  
FROM MEMBER  
WHERE EXTRACT(MONTH FROM TO_DATE(BIRTHDAY, 'YYYY-MM-DD')) IN ('2', '3', '11', '12');  

&nbsp;
#### ♠EX) 가입한 회원중에 가입한지 6개월이 안되는 회원을 조회하시오
1) ADD_MONTHS 사용  
WHERE ADD_MONTHS(SYSDATE, -6) < REGDATE;

4) MONTHS_BETWEEN(날짜, 날짜) : 날짜의 차이를 알아내는 함수  
WHERE MONTHS_BETWEEN(SYSDATE, REGDATE) < 6; --이렇게 할 수도 있당  




    
&nbsp;
&nbsp;

## ※형식변환 함수

![형식변환함수](https://user-images.githubusercontent.com/43837994/154638391-624af7dc-6c5c-4929-889c-eca0c48f7067.PNG)

&nbsp;
&nbsp;

### 1. TO_CHAR()
> NUMBER, DATE ▶ VARCHAR2
TO_CHAR(number)

#### ♠EX) 
* TO_CHAR(number, '$99,999,999') ▶뒤의 형식은 숫자보다 길어야함.  
* select TO_CHAR(123, '9999,9') || 'hello' ▶ 공백이 빈칸으로 나오게된다. ▶     _____12,3hello(_은 공백)  
▶공백을 없애고 싶으면 trim함수를 써도 된다.

&nbsp;
**TO_CHAR에서 NUMBER▶STRING로 바꿀때 쓰일 포맷문자 형식**  
![to_char에서 포맷문자 형식](https://user-images.githubusercontent.com/43837994/154638698-9966197c-a442-4a79-abb6-7adcc86fcae3.PNG)

&nbsp;
**TO_CHAR에서 DATE▶STRING로 바꿀때 쓰일 포맷문자 형식**
![to_Date 포맷문자형식](https://user-images.githubusercontent.com/43837994/154639836-3e0352ff-209b-46f1-a7a6-a7ed09448db8.PNG)

