## ※집계함수
    SUM, MIN, MAX, COUNT, AVG
    
```
COUNT()결과에 NULL이 포함되는경우
  포함되는 경우 : COUNT(*)
  포함되지 않는 경우: COUNT(ColumnName)
```

> 하지만, 빈 문자열은 COUNT() 결과에 포함됩니다.   
> **빈 문자열을 COUNT() 결과에서 빼려면 빈 문자열을 NULL로 바꾸고 COUNT()를 하면 됩니다.**   
    mysql : COUNT( IF (ColumnName=”, NULL, ColumnName)     
    mssql : COUNT( CASE WHEN ColumnName=” THEN NULL ELSE ColumnName END )  
    
    COUNT( DISTINCT( ColumnName ) )으로 하면 중복되지 않고 NULL은 제외되는 값들만 COUNT 하게 됩니다.

## ※그룹함수
    ROLLUP, GROUPING SETS, CUBE 함수

1. ROLLUP  
그룹화 컬럼들에 대한 계층적 소계를 생성해주는 함수.
&nbsp;
![image](https://github.com/Kangchaemin/SQL_Rule/assets/43837994/9b9b248d-2ca7-4dff-b922-50a34be5bba5)

```
ROLLUP함수는 인수의 순서에도 영향을 받게 된다.
```

2. GROUPING SETS  
    GROUPING SETS는 특정 항목에 대한 소계를 계산하는 함수입니다.
   
&nbsp;
![image](https://github.com/Kangchaemin/SQL_Rule/assets/43837994/187e3d09-0cfc-41ac-b1c1-893035be6fab)  

![image](https://github.com/Kangchaemin/SQL_Rule/assets/43837994/f33fac04-1ff4-41e5-9f62-19526823ea03)

3. CUBE  
결합 가능한 모든 그룹에 대하여 다차원 집계 및 소계를 생성해주는 함수.

&nbsp;
![image](https://github.com/Kangchaemin/SQL_Rule/assets/43837994/ed06dc44-294e-4520-a274-7a42334a9102)  
ROLLUP 함수와는 다르게 인자의 순서가 달라도 결과는 같다.  
위와 다르게 단순한 월별 소계(SUBTOTAL)도 생성되었으며, 그룹핑 컬럼의 개수를 N이라고 한다면 2의 N승의 소계(SUBTOTAL)을 생성한다.


## GROUPING
 오라클의 GROUPING, GROUPING_ID 함수는 소계와 합계를 집계할 때 사용하는 ROLLUP, CUBE, GROUPING SETS 함수와 함께 사용된다.    

&nbsp;
![image](https://github.com/Kangchaemin/SQL_Rule/assets/43837994/fa8c273b-511e-4d7a-ba0b-984f823c3cda)


```
GROUPING 함수는 소계, 합계로 집계된 행의 컬럼 NULL을 구분할 수있다.  
NULL인 경우 1을 반환하고 아닌경우 0을 반환한다.
```
