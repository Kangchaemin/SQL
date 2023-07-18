/*AND A.DESIGN_NO NOT IN ( SELECT DESIGN_NO  /* 설계번호 */ 
                                               FROM GL_BSN_REPRATN_CTRT /*영업배상계약_기본정보 : ELDEGN22*/
                                              WHERE DESIGN_NO  /* 설계번호 */ = A.DESIGN_NO  /* 설계번호 */ )	*/



-> LEFT JOIN으로 내리는 법
LEFT JOIN GL_BSN_REPRATN_CTRT B /*영업배상계약_기본정보 : ELDEGN22*/
                               ON B.DESIGN_NO = A.DESIGN_NO  /* 설계번호 */
하고 밖 WHERE 조건에 

WHERE B.DESIGN_NO IS NULL
