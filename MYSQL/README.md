# 1. Math 함수

## ✨MOD(분자, 분모) = %
> 분자를 분모로 나눈 나머지를 구한다

## ✨소수
- CEILING : 올림
- FLOOR : 내림
- TRUNCATE(숫자, 자릿수) : 소수점 이하 자릿수에서 버림 (버릴 자릿수 까지만 살림)
- ROUND(숫자, 자릿수) : 소수점 이하 자릿수에서 반올림 ( 자릿수 + 1의 자리에서 반올림)

**EX)**
> ROUND(12.56, 1) // 12.  
ROUND(12.56, -1) // 1의 자리 반올림 // 10

* * *
# 2. 문자열

## ✨CONCAT(문자열, 문자열) : 문자열 더하기

## ✨CHAR_LENGTH(문자열) : 문자열 길이

## ASCII('A') -> 65 / CHAR(65) -> 'A'

## UPPER() / LOWER()

## ✨SUBSTRING(문자열, 시작위치, 길이) : (문자열의 INDEX는 1부터 시작)
<pre>
  SELECT SUBSTRING('123456789', 7);  // 789

  SELECT SUBSTRING('123456789', -7);  // 3456789
</pre>

## ✨SUBSTRING_INDEX(문자열, 구분자, 구분자 Index)
<pre>
  SELECT SUBSTRING_INDEX('사과,바나나,딸기,포도', ',', 3);
  >> 사과,바나나,딸기

  SELECT SUBSTRING_INDEX('사과,바나나,딸기,포도', ',', -3);
  >> 바나나,딸기,포도
</pre>
## ✨LEFT(문자열, 길이) / RIGHT(문자열, 길이) : 왼쪽~길이만큼 / 오른쪽~길이만큼 끊어준다.

## ✨LOCATE(찾고자 하는 문자열, 문자열) : 찾고자 하는 문자가 나온 첫번째 위
<pre>
  SELECT LOCATE('A', 'ABC') // 1
</pre>

* * *
# 3. 3자리마다 , FORMAT(컬럼명, 0) // (뒤에 숫자는 끊어낼 자릿수)

* * *
# 4. 날짜

## ✨현재 날짜
> NOW()     - 현재 날짜 + 시간  // YYYY-MM-DD HH:MM:SS
> CURDATE() - 현재 날짜만       // YYYY-MM-DD
> CURTIME() - 현재 시간만       // HH:MM:SS

## ✨DATE_FORMAT(DATE, FORMAT) : DATE -> CHAR타입으로 변경됨.
<pre>
  SELECT DATE_FORMAT(hiredate, '%Y-%m-%d') FROM emp;
  -- YYYY-mm-dd 
  
  SELECT DATE_FORMAT(hiredate, '%Y-%m-%d %T') FROM emp;
  SELECT DATE_FORMAT(hiredate, '%Y-%m-%d %H:%i:%s') FROM emp;
  -- YYYY-mm-dd 00:00:00
</pre>

## ✨DAYOFWEEK(date) - 주어진 date의 일자가 해당 주에서 몇 번째 날인지 반환(일요일=1, 토요일=7)
<pre>
  SUBSTR('일월화수목금토', DAYOFWEEK(DATE), 1)
</pre>

## ✨ADDDATE(날짜, INTERVAL 숫자 DAY/MONTH,,)
<pre>
  SELECT ADDDATE('1998-01-02', INTERVAL 42 DAY);    // 42일를 더한 값을 반환받습니다.
  SELECT DATE_ADD('1998-01-02', INTERVAL 1 MONTH);  // 1달를 더한 값을 반환받습니다.
</pre>

## ✨DATEDIFF(date1, date2)
date1 - date2 : 일로 반환
