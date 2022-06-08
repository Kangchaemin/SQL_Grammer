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
