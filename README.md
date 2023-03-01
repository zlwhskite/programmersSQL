# programmersSQL
출처: 프로그래머스 코딩 테스트 연습, https://school.programmers.co.kr/learn/challenges
---
- 프로그래머스 Lv1 조건에 맞는 회원수 구하기
    ->USER_INFO 테이블에서 2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원이 
        몇 명인지 출력하는 SQL문을 작성해주세요.

###### 
        SELECT COUNT(USER_ID) AS USERS FROM USER_INFO WHERE AGE BETWEEN 20 AND 29 AND YEAR(JOINED) = 2021
    
    
        - YEAR()함수 : 정수값을 반환함
        - MONTH()
        - DATE()


- 프로그래머스 Lv1 가장 비싼 상품 구하기
    ->PRODUCT 테이블에서 판매 중인 상품 중 가장 높은 판매가를 출력하는 
        SQL문을 작성해주세요. 이때 컬럼명은 MAX_PRICE로 지정해주세요.
        
###### 
        SELECT MAX(PRICE) AS MAX_PRICE FROM PRODUCT


- 프로그래머스 Lv2 재구매가 일어난 상품과 회원 리스트 구하기
    ->ONLINE_SALE 테이블에서 동일한 회원이 동일한 상품을 재구매한 데이터를 구하여, 재구매한 회원 ID와 재구매한 상품 ID를 출력하는 SQL문을 작성해주세요. 
        결과는 회원 ID를 기준으로 오름차순 정렬해주시고 회원 ID가 같다면 상품 ID를 기준으로 내림차순 정렬해주세요.
        
###### 
        SELECT USER_ID, PRODUCT_ID FROM ONLINE_SAIL
        GROUP BY USER_ID, PRODUCT_ID
        HAVING COUNT(USER_ID) >= 2
        ORDER BY USER_ID ASC, PRODUCT_ID DESC 
