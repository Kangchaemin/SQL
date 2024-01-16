## 1. 기본키 한개일 경우
- 윈도우 함수 사용
<pre>
  SELECT student_id,
         ROW_NUMBER() OVER (ORDER BY student_id) AS seq
    FROM Weights;
</pre>
- 상관 서브쿼리
<pre>
  SELECT student_id
         (SELECT COUNT(*)
            FROM Weights W2
           WHERE W2.student_id <= W1.student_id) AS seq
    FROM Weights W1;
</pre>
![image](https://github.com/Kangchaemin/SQL/assets/43837994/36cb46d6-2b50-4966-acc4-834edc9f1949)

## 2. 그룹마다 순번을 붙이는 경우 
- 윈도우 함수 사용
<pre>
  SELECT class, student_id,
         ROW_NUMBER() OVER (PARTITION BY class ORDER BY student_id) AS seq
    FROM Weights W2;
</pre>
- 상관 서브쿼리
<pre>
  SELECT class, student_id,
         (SELECT COUNT(*) 
            FROM Weights W2
           WHERE W2.class = W1.class
             AND W2.student_id <= W1.student_id) AS seq
    FROM Weights2 W1;
</pre>
![image](https://github.com/Kangchaemin/SQL/assets/43837994/16a9b293-bca4-49c9-bcdc-4c19c7f549ce)

* * * 
## 3. 응용 - 중앙값 구하기
- 윈도우 함수 사용
<pre>
  SELECT AVG(weight)
    FROM (SELECT weight,
                 2 * ROW_NUMBER() OVER (ORDER BY weight)
                   - COUNT(*) OVER() AS diff
            FROM Weights) TMP
    WHERE diff BETWEEN 0 AND 2;
</pre>
마지막 필드 diff는 2 * ROW_NUMBER() - COUNT(*) 입니다.  
이후에 diff가 0~2인 값을 찾고 평균을 구하는 것입니다.
![image](https://github.com/Kangchaemin/SQL/assets/43837994/7210d0c4-fddc-49db-88ee-bdcc26d6d341)

