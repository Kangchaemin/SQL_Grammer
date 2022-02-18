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
##### EX) 조회수가 0, 2, 7인 게시글을 조회하시오

WHERER 조회수 == 0 OR .... ▶ 비효휼적.   
> 따라서 IN을 쓴다. : WHERE 조회수 IN(0, 2, 7);

&nbsp;
NOT을 쓸려면 WHERE 조회수 NOT IN(0, 2, 7) : 0, 2, 7만 빼고.
-.> IN절 안에 SELECT절이 추가로 들어갈 수 있다. 

## ※LIKE, %  
> _은 한문자 / %는 모든문자. 

##### EX) *회원 중에서 '박'씨 성을 조회하시오.
WHERE 회원이름 LIKE '박%';  
> ★--회원이름 = '박%' : 이렇게 하면 진짜 박%를 찾게된다. 

## ※ALL_TAB_COMMENTS
> all_tab_comments : 테이블에 관련된 정보를 한눈에 볼 수 있다.
all_tables작성방법

> comment를 달았기때문에 정보를 참고할 수 있다.
FROM all_col_comments WHERE comments LIKE ~~쓰면 된다.   

**정규식도 참고해보면 좋다.

## ※정규식
```sh






```
