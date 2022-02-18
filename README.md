# _SQL_Grammer_
&nbsp;
## ※DDL, DML, DCL에 관련해서

| Plugin | 종류 |
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

## ※CHARACTER 형식

#### ▶Oracle에서는 문자열을 '' 으로 표시한다. (""아님!)

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
#### EX) 조회수가 0, 2, 7인 게시글을 조회하시오

WHERER 조회수 == 0 OR .... ▶ 비효휼적.   
> 따라서 IN을 쓴다. : WHERE 조회수 IN(0, 2, 7);

&nbsp;
NOT을 쓸려면 WHERE 조회수 NOT IN(0, 2, 7) : 0, 2, 7만 빼고.
-.> IN절 안에 SELECT절이 추가로 들어갈 수 있다. 

&nbsp;
&nbsp;
## ※LIKE, %  
> _은 한문자 / %는 모든문자. 

##### EX) *회원 중에서 '박'씨 성을 조회하시오.
WHERE 회원이름 LIKE '박%';  
> ★--회원이름 = '박%' : 이렇게 하면 진짜 박%를 찾게된다. 

&nbsp;
&nbsp;

## ※ALL_TAB_COMMENTS
> all_tab_comments : 테이블에 관련된 정보를 한눈에 볼 수 있다.
all_tables작성방법

> comment를 달았기때문에 정보를 참고할 수 있다.
FROM all_col_comments WHERE comments LIKE ~~쓰면 된다.   

**정규식도 참고해보면 좋다.

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
##### EX) 회원중에서 전화번호가 011로 시작하는 회원의 정보 출력
WHERE SUBSTR(PHONE, 1, 3) = '011'; -> 함수를 쓰는것이 속도문제에서 걸린다.  
WHERE PHONE LIKE '011%' -> 이렇게 하는것이 더 바람직하다.  
> LIKE가 먼저다 라는 생각을 항상 가지고 있으면 좋다.

##### EX) 회원중에서 생년월일이 7, 8, 9월인 회원정보 출력 
SELECT * FROM MEMBER WHERE PHONE IS NULL AND SUBSTR(BIRTHDAY, 6, 2) IN (7, 8, 9);  
SELECT * FROM MEMBER WHERE PHONE IS NULL AND SUBSTR(BIRTHDAY, 6, 2) IN ('07', '08', '09');

&nbsp;
### ◎문자열 덧셈 함수
    CONCAT('홍', '길동')

    <<문자열 연산
    3 + '4'
    3 || '4' -> 연산자로 쓰는것이 성능이 더 빠르다. 

&nbsp;
### ◎TRIM 함수 : 빈공백을 없애주는 함수
    LTRIM -> 왼쪽공백만  
    RTRIM  
    TRIM -> 양쪽의 빈공백을 없애준다  

&nbsp;
### ◎ 모두 대소문자로 변경하기
    LOWER('AFJDFKDJKF  
    UPPER

##### EX) 회원의 아이디가 'NEWR'인 사람을 조회하시오(대소문자 상관없이)  
SELECT * FROM MEMBER WHERE UPPER(NAME) = 'jjj';  

##### ex) 이름과 생년월일에서 -을 뺀것을 출력하시오  
SELECT NAME, REPLACE(BIRTHDAY, '-', '') FROM MEMBER;   

&nbsp;
### ◎ LPAD, RPAD도 알아두기. (문자열 함수에서) 
