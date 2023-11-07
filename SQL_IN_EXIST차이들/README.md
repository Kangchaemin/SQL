#### 참고할 자료
https://doorbw.tistory.com/222

#### 1. IN
<pre>
  SELECT * FROM TB_FOOD fWHERE f.number IN (SELECT c.number FROM TB_COLOR c);
</pre>

IN의 경우 제일 먼저 TB_COLOR 테이블에 접근하게 된다.  
IN 뒤에있는 서브쿼리를 먼저 실행해서 그에 대한 요소를 가져온 후  
TB_FOOD 테이블의 레코드를 하나씩 가져오면서 그 레코드의 number의 값이 IN()에 있는지 확인한다.  

#### 2. EXISTS
<pre>
  SELECT * FROM TB_FOOD fWHERE f.number IN (SELECT c.number FROM TB_COLOR c);
</pre>

> IN구문에서는 IN 이후에 나오는 소괄호 내부의 서브쿼리에 대해서 먼저 접근하였습니다. 하지만 EXISTS 구문에서는 다릅니다.  
> <b> 먼저 TB_FOOD에 접근하여 하나의 레코드를 가져오고 그 레코드에 대해서 EXISTS 이하의 서브쿼리를 실행하고 서브쿼리에 대한 결과가 '존재하는지'를 확인합니다. </b>

예시를 들어 생각해보면, 제일 처음에 [ 1 / 치킨 ] 이라는 레코드를 가져왔을 것이고, 해당 레코드에 대해서 SELECT c.number FROM TB_COLOR c 쿼리를 통해 결과가 나오는지 확인합니다.  
이때 서브쿼리에 대해 어떠한 결과라도 존재하기만 한다면 참이 되어서 [ 1 / 치킨 ] 레코드가 출력됩니다.  
그런데 SELECT c.number FROM TB_COLOR c 쿼리는 사실 TB_FOOD의 어떠한 레코드하고도 연관이 없이 항상 결과값을 가지는 쿼리입니다. 따라서 TB_FOOD의 모든 레코드가 출력되는 것 이죠.

<pre>
  SELECT * FROM TB_FOOD fWHERE EXISTS (SELECT c.number FROM TB_COLOR c WHERE c.number = f.number);
</pre>

해당 쿼리의 결과는 위의 IN과 동일하지만 <b> 내부적으로 쿼리가 동작하는 방식은 아얘 다르다. </b>

#### 3. 이하 NOT IN, NOT EXIST 동일하다.
