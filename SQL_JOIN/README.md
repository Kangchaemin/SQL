# _JOIN에 대해서_

| JOIN | 정의 |
| ------ | ------ |
| INNER | 관계가 있는것만 조인 |
| OUTER | 관계가 없는것만 조인 |


- OUTER : LEFT / RIGHT / FULL

&nbsp;
```sh
RIGHT = 오른쪽에 있는 아우터를 포함하겠다  
LFET = 왼쪽에 있는 ~~   
FULL = 모든걸 포함하겠다  
▶ 현업때는 LEFT JOIN을 쓴다. (LEFT 거를 앞에 master로 둔다.)  
▶ Table에서도 Alias를 많이 쓴다. 
```

## ※ INNER JOIN
> 관계가 있는것끼리만 묶는 것이다.

![전체 컬럼](https://user-images.githubusercontent.com/43837994/154605507-5dc0f604-945b-4588-8936-ae3070d4dcb3.PNG)

위에있는 사진을 inner join한다고 생각해보면  
inner join은 **관계가 있는것끼리만** 묶기 때문에 결과를 보면  
![innerjoin 결과](https://user-images.githubusercontent.com/43837994/154606025-658a1332-8add-4930-a110-3a8387559c07.PNG)  
이렇게 되며 컬럼은 3개이다. 
&nbsp;
#### inner join 쿼리 
SELECT *  
FROM MEMBER  
**INNER JOIN** NOTICE **ON** MEMBER.ID = NOTICE.WRITER_ID;

&nbsp;
&nbsp;

## ※ OUTER JOIN
> 관계가 없는것끼리만 묶는 것이다.

&nbsp;
### 1.LEFT JOIN
왼쪽이 기준이 되는것이며 오른쪽과 합쳐질때 값이 없는것은 null로 표시가된다.  
![left join 결과](https://user-images.githubusercontent.com/43837994/154606738-7fdf5584-8f3b-4672-9980-9374a4b1680b.PNG)
&nbsp;
#### ◎left join 쿼리   
SELECT *  
FROM NOTICE N  
**LEFT OUTER JOIN** MEMBER M **ON** N.WRITER_ID = M.ID;  
▶ 이때 LEFT가 NOTICE가 되는 것이다. 멤버테이블에 존재하지않는건 NULL로 표시된다.
&nbsp;

### 2.RIGHT JOIN
오른쪽이 기준이 되는것이며 왼쪽과 합쳐질때 값이 없는것은 null로 표시가된다.  
![right join 결과](https://user-images.githubusercontent.com/43837994/154607358-445e516a-e41b-4693-ba89-09fb5875a5a1.PNG)
&nbsp;
#### ◎right join 쿼리   
SELECT *  
FROM NOTICE N  
**RIGHT OUTER JOIN** MEMBER M **ON** N.WRITER_ID = M.ID;  
&nbsp;

### 2.FULL JOIN
![full join 결과](https://user-images.githubusercontent.com/43837994/154614576-2aa7464a-2f9f-4bea-8a3d-a68e9da75924.png)
#### ◎full join 쿼리   
SELECT *  
FROM NOTICE N  
**FULL OUTER JOIN** MEMBER M **ON** N.WRITER_ID = M.ID;  
&nbsp;

### 3.SELF JOIN
#### ◎self join 쿼리   
SELECT M.*, B.NAME AS BOSS_NAME  
FROM **MEMBER M**   
LEFT OUTER JOIN **MEMBER B** ON B.ID = M.BOSS_ID; 
#### ♠EX) ID, NAME 그리고 회원별 작성한 게시글 수를 조회하시오. 

SELECT M.ID, M.NAME, COUNT(N.ID)   
FROM MEMBER M   
INNER JOIN NOTICE N ON M.ID = N.WIRTER_ID  
GROUP BY M.ID, M.NAME   
▶COUNT를 하기 위해 앞에 컬럼을 한개만 주기 위해서 GROUP BY로 조인해줬다. 
> INNER JOIN하면서 COUNT가 0인 회원이 없어졌다.  
&nbsp;
이럴 경우? OUTER JOIN을 하게되면 주인공(MASTER)를 잡는것이다. 

&nbsp;
### 3.ORACLE JOIN
INNER JOIN은  
FROM MEMBER M, NOTICE N 이렇게 나열.  
_추가적인 필터링은 AND로 묶는다._ 

>OUTER JOIN을 할려면
FROM NOTICE N, MEMBER M
WHERE N.WRITER_ID = M.ID(+)
