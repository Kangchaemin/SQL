# _정규식_

&nbsp;
## 참고하면 좋을 사이트
> ★Regular Expression Library  
https://regexlib.com/  
여기서 CheatSheet으로 들어가기

&nbsp;

![정규식_캡처1](https://user-images.githubusercontent.com/43837994/154871347-86f9aa12-c4f2-436f-b5c1-1211d4094a11.PNG)



![정규식_캡처2](https://user-images.githubusercontent.com/43837994/154871373-b99e42e2-7ca9-4a0b-bfa1-d77edcc4ce1d.PNG)

&nbsp;

## ※ 위를 참고해서 정규식 표현을 만들어보자.

#### ♠EX)  Title에 번호가 포함되어있는지 확인.

1) WHERE title LIKE '%-%-%'; ▶ %는 문자든 숫자든 다 포함한다.  
**※전화번호만 입력되게 할려면 3글자 4글자 4글자 패턴으로 써야한다**

> [012] : 0또는 1또는 2또는...   
\d : [0-9]를 나타내준다.  
{..} : 반복되는 숫자를 나타낸다 ▶ab{2}c == abbc  
{3, 4} : 3개 또는 4개가 반복된다. 

2) 01[01]-\d\d\d\d-\d\d\d\d -- **너무 정신없음**

3) [01[01]-\d{3,4}-\d{4}

#### ★정규식을 절에 포함할때는 
WHERE LIKE '01[01]-\d{3,4}..' ▶X  
WHERE **REGEXP_LIKE(title, 정규식)** ▶ O


&nbsp;

#### ♠EX)  이메일 형식 정규식 표현
아무문자@문자.com, .org, .net표현이라면  

1) @앞에는 문자 한개이상이 들어가야한다.  
[0-9a-zA-Z] ▶한계가 있어보인다. 
> \w : [0-9a-zA-Z]
\w+@ : 문자가 한개이상 오고 @가 온다는 뜻이다.  
| : 'OR'개념으로 묶어주는 연산자.

2) \w+@\w+.(org|net|com)  
▶위 정답은 11@1na.com같은 숫자가 앞에 포함된 것도  포함한다.  

> 앞에는 숫자가 못오게 설정할려면  
\D : [^0-9] : 0부터 9까지의 숫자가 ^(아닌)걸로 시작

3) \D\w+@\D\w+.(org|net|com)
