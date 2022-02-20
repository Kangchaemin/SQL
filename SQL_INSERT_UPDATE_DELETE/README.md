# _SQL INSERT / UPDATE / DELETE_

## 1. INSERT문

1. 모든 필드값 입력하기  
INSERT INTO 테이블 VALUES(' ', ' ', ...)

2. 원하는 필드만, 원하는 순서대로 입력하기  
INSERT INTO 테이블(id, pwd) VALUES('ddd', '111') ▶나머지 필드값에는 NULL이 들어가게 된다. 

&nbsp;
## 2. UPDATE문

1. 모든 행의 pwd를 '111'로 변경하기  
UPDATE 테이블 SET pwd='111'

2. 특정 user에 대해서 바꾸고싶을때는 **조건절 where를 사용한다**  
UPDATE 테이블 SET pwd='111' WHERE id='123'

3. 모든 행의 pwd를 '111'과 이름도 바꾸고싶으면 ,로 구분해서 넣어준다.  
UPDATE 테이블 SET pwd='111', name='손오공' 

&nbsp;
## 3. DELETE문

1. DELETE 테이블 ▶ 전체 테이블 날림
2. DELETE 테이블 WHERE id='test' ▶ 조건지정
