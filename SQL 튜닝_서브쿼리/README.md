## 예제 1. 고객별 최소 순번(seq) 구하기 (단 seq는 오래될 수록 작은값 가짐)
<pre>
  SELECT R1.custid, R1.seq, R1.price
    FROM Receipts R1
         INNER JOIN ( SELECT cust_id, MIN(seq) AS min_seq
                        FROM Receipts
                       GROUP BY cust_id) R2
                 ON R1.cust_id = R2.cust_id
                AND R1.seq     = R2.min_seq;
</pre>

서브쿼리가 좋지 않은 이유
- 일시적인 영역에 확보되므로 오버헤드가 생긴다.
- 이 쿼리는 결합을 필요로 하기 때문에 비용이 높고 실행 계획 변동 리스크가 발생한다.
- Receipts 테이블에 스캔이 두번 필요하다.

![KakaoTalk_20240115_103248167](https://github.com/Kangchaemin/SQL_Rule/assets/43837994/712e154e-70a0-4380-b997-3ba713b14ea6)

&nbsp;
해당 부분의 개선점 'Receipts 테이블에 대한 접근을 1회로 줄이기' 입니다.
> 개선한 코드와 테이블
&nbsp;
![image](https://github.com/Kangchaemin/SQL_Rule/assets/43837994/552e08b4-c9db-4102-8aed-d0b162e9d576)
