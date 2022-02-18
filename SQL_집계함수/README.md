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
