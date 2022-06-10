# SQL 문제 풀면서 몰랐던것들 

#### ♣'boring' 이라는 문자열을 제외하고 출력하기 
  description not like 'boring'
  description != 'boring'
  
  
&nbsp;  
#### ♣2개이상 중복되는 컬럼명만 보여줄때 

▶ 흔히 중복되는 값을 빼고 보여줄때는 distinct를 통해 보여준다.  
하지만 중복되는 컬럼명만 보여줘야 할때는 group by를 통해 묶어줘서 보여줘야한다. 

ex) email이 2번 중복되는 컬럼만 보여주시오. 
  SELECT email FROM person
  GROUP BY email
  HAVING count(id) >= 2  
  
★ group by를 연산한 컬럼을 가지고 필터링 하고싶을때는 having 절을 사용하면 된다. 



&nbsp;  
#### ♣문자열의 시작과 끝을 확인해아할때 

▶ 문자열의 시작과 끝이 모음이 아닌 경우를 출력하는경우에는  
WHERE LEFT(CITY, 1) NOT IN ('A', 'E', 'I', 'O', 'U')
      OR RIGHT(CITY, 1) NOT IN ('A', 'E', 'I', 'O', 'U');  
이렇게 해주면 된다. 


&nbsp;  
#### ♣GROUP BY 사용시 SELECT 절 
> GROUP BY를 사용하는 경우, SELECT할 수 있는 컬럼은 GROUP BY에 나열된 컬럼과 SUM(), COUNT() 같은 집계 함수(Aggregation Function)으로 한정 
