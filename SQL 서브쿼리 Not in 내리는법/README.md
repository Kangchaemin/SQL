#### 1. 
<pre>
/*AND A.DESIGN_NO NOT IN ( SELECT DESIGN_NO  /* 설계번호 */ 
                                               FROM GL_BSN_REPRATN_CTRT /*영업배상계약_기본정보 : ELDEGN22*/
                                              WHERE DESIGN_NO  /* 설계번호 */ = A.DESIGN_NO  /* 설계번호 */ )	*/



-> LEFT JOIN으로 내리는 법
LEFT JOIN GL_BSN_REPRATN_CTRT B /*영업배상계약_기본정보 : ELDEGN22*/
                               ON B.DESIGN_NO = A.DESIGN_NO  /* 설계번호 */
하고 밖 WHERE 조건에 

WHERE B.DESIGN_NO IS NULL

</pre>

#### 2. 
<pre>

  SELECT C.컨텐츠ID, C.컨텐츠명
  FROM 고객 A
       INNER JOIN 추천컨텐츠 B
               ON A.고객ID = B.고객ID
       INNER JOIN 컨텐츠 C
               ON B.컨텐츠ID = C.컨텐츠ID
       LEFT OUTER JOIN 비선호콘텐츠 D
               ON B.고객ID = D.고객ID 
              AND B.컨텐츠ID = D.컨텐츠ID
  WHERE A.고객ID = #custid#
    AND B.추천대상일자 = TO_CHAR(SYSDATE, 'YYYY.MM.DD')
    AND D.컨텐츠ID IS NULL

  -> LEFT JOIN으로 내리는 법
  
  SELECT C.컨텐츠ID, C.컨텐츠명
  FROM 고객 A
       INNER JOIN 추천컨텐츠 B
               ON A.고객ID = #custid#
              AND A.고객ID = B.고객ID
       INNER JOIN 컨텐츠 C
               ON B.컨텐츠ID = C.컨텐츠ID
       LEFT OUTER JOIN 비선호콘텐츠 D
               ON B.고객ID = D.고객ID 
              AND B.컨텐츠ID = D.컨텐츠ID
  WHERE B.추천대상일자 = TO_CHAR(SYSDATE, 'YYYY.MM.DD')
    AND NOT EXISTS ( SELECT X.컨텐츠ID 
                       FROM 비선호컨텐츠 X
                      WHERE X.고객ID = B.고객ID
                        AND X.컨텐츠ID = B.컨텐츠ID )
  
</pre>
