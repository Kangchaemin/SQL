![KakaoTalk_20240118_172239815](https://github.com/Kangchaemin/SQL/assets/43837994/0aadb5c3-3bf1-4eeb-9a09-e5ab32cc0f63)
![KakaoTalk_20240118_172117333_02](https://github.com/Kangchaemin/SQL/assets/43837994/3fc58a6c-3f2b-41ce-b918-3261343c8466)

* * *
## 주문일(order_date)과 상품의 배송예정일(delivery_date)의 차이를 구해 3일 이상이라면 주문자에게 **배송주문이 늦어지고 있다는 연락을 하고 싶습니다.**

* * *
### 주문번호별 최대 지연일을 알고싶다면 주문번호를 집약할 수 있다.
<pre>
  SELECT O.order_id,
         MAX(O.order_name),
         MAX(B.delivery_date - O.order_date) AS max_diff_days
    FROM Orders O
         INNER JOIN OrderRecipts B
                 ON O.order_id = B.order_id
   WHERE B.delivery_date - O.order_Date >= 3
   GROUP BY O.order_id;
</pre>

> 여기서 O.order_name에 MAX 함수를 적용한 것은 딱히 최댓값을 구하려는게 아니라 **SELECT구문에 order_name필드를 그냥 입력할 수 없기 때문입니다.**  
> order_name 필드는 상수도 아니고, GROUP BY 구에서도 사용하지 않습니다. 따라서 그대로 SELECT 구문에 적으면 오류가 발생하니다.  
> 이를 방지하고자 집약 함수의 형태로 사용한 것뿐입니다.  
따라서 MIN함수를 작성하여도 됩니다.  

> order_id와 order_name이 1:1 조건이 성립한다면 GROUP BY절에 order_id, order name을 입력해도 됩니다.  
> 이렇게 하면 order_name에 MAX를 하지 않아도 됩니다.
