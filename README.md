# _SQL_Grammer_




## DDL, DML, DCL에 관련해서
- DDL : CREATE / ALTER / DROP
- DML : SELECT / INSERT / UPDATE / DELETE
- DCL : GRANT / REVOKE

## CDB와 XEPDB는?

## CHARACTER 형식

### Oracle에서는 문자열을 ''으로 표시한다. (""아님!)

'''sh
1) CHAR : CHAR(50)처럼 쓰며 50의 공간을 쓰지않아도 50개의 공간을 차지하고있다. 따라서 고정길이일때 사용하는것이 좋다. (가변길이 적함X)
2) VARCHAR2 : VARCHAR2(50) 처럼 쓰며 괄호안에 숫자는 최대길이의 숫자를 지정해주면 된다. (가변길이 적합O)
3) NCHAR : ???
'''

## DATE, TIMESTAMP 형식
- DATE : '2013-02-15' 형식
- TIMESTAP : 'DATE형식 + 시분초까지'

## OR, AND, BETWEEN, IN
### IN을 쓰는것이 속도에 더 좋다. 

#### 조회수가 0, 1, 2인 게시글을 조회하시오
WHERE 조회수 = 0 OR 조회수 = 1 ....
