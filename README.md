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
        
        
        - ASC 오름차순 ex)1, 2, 3, 4 .....
        - DESC 내림차순 ex) 5, 4, 3, 2 .....
        
     
- 프로그래머스 Lv1 흉부외과 또는 일반외과 의사 목록 출력하기
    ->DOCTOR 테이블에서 진료과가 흉부외과(CS)이거나 일반외과(GS)인 의사의 이름, 의사ID, 진료과, 고용일자를 조회하는 SQL문을 작성해주세요. 
        이때 결과는 고용일자를 기준으로 내림차순 정렬하고, 고용일자가 같다면 이름을 기준으로 오름차순 정렬해주세요.
     
######
        SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD,'%Y-%m-%d') 
        FROM DOCTOR
        WHERE MCDP_CD = 'CS' OR MCDP_CD = 'GS' 
        ORDER BY HIRE_YMD DESC, DR_NAME  ASC 
        
        
        - DATE_FORMAT() y대문자주의
         
         
 - 프로그래머스 Lv1 과일로 만든 아이스크림 고르기 
    ->상반기 아이스크림 총주문량이 3,000보다 높으면서 아이스크림의 주 성분이 과일인 아이스크림의 맛을 총주문량이 큰 순서대로 조회하는 SQL 문을 작성해주세요.

######
        SELECT FLAVOR FROM FIRST_HALF 
        JOIN ICECREAM_INFO ON FIRST_HALF.FLAVOR = ICECREAM_INFO.FLAVOR
        WHERE ICECREAM_INFO.INGREDIRNT_TYPE = 'fruit_based' 
        AND TOTAL_ORDER > 3000
        ORDER BY TOTAL_ORDER DESC
        
        - 순서 : FROM -> ON -> JOIN -> WHERE -> GROUP BY -> HAVING -> SELECT
        
        
 - 프로그래머스 Lv1 동물의 아이디와 이름
    ->동물 보호소에 들어온 모든 동물의 아이디와 이름을 ANIMAL_ID순으로 조회하는 SQL문을 작성해주세요.
    
 ######
        SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
        ORDER BY ANIMAL_ID ASC      
        
        
 - 프로그래머스 Lv2 상품 별 오프라인 매출 구하기
    ->PRODUCT 테이블과 OFFLINE_SALE 테이블에서 상품코드 별 매출액(판매가 * 판매량) 합계를 출력하는 SQL문을 작성해주세요. 
        결과는 매출액을 기준으로 내림차순 정렬해주시고 매출액이 같다면 상품코드를 기준으로 오름차순 정렬해주세요.
    
######
        SELECT PRODUCT_CODE, SUM(PRODUCT.PRICE * OFFLINE_SALE.SALES_AMOUNT) AS SALES FROM PRODUCT
        JOIN OFFLINE_SALE ON PRODUCT.PRODUCT_ID = OFFLINE_SALE.PRODUCT_ID
        GROUP BY PRODUCT_CODE
        ORDER BY SALES DESC, PRODUCT_ID ASC
        
     
- 프로그래머스 Lv2 조건에 맞는 도서와 저자 리스트 출력하기
    ->'경제' 카테고리에 속하는 도서들의 도서 ID(BOOK_ID), 저자명(AUTHOR_NAME), 출판일(PUBLISHED_DATE) 리스트를 출력하는 SQL문을 작성해주세요. 
        결과는 출판일을 기준으로 오름차순 정렬해주세요.
        
######
        
        SELECT BOOK_ID, AUTHOR_NAME, PUBLISHED_DATE 
        FROM BOOK 
        JOIN AUTHOR ON BOOK.AUTHOR_ID = AUTHOR.AUTHOR_ID
        WHERE CATEGORY = '경제' ORDER BY PUBLISHED_DATE
        
        
- 프로그래머스 Lv3 없어진 기록 찾기
    ->천재지변으로 인해 일부 데이터가 유실되었습니다. 입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 
        ID와 이름을 ID 순으로 조회하는 SQL문을 작성해주세요.
        
######
        SELECT ANIMAL_OUTS.ANIMAL_ID, ANIMAL_OUTS.NAME 
        FROM ANIMAL_OUTS
        LEFT JOIN ANIMAL_INS 
        ON ANIMIAL_OUTS.AMNIMAL_ID = ANIMAL_INS.AMNIMAL_ID
        WHERE ANIMAL_INS.ANIMAL_ID IS NULL
        ORDER BY ANIMAL_OUTS.ANIMAL_ID ASC
        
        
- 중복된 데이터 하나씩 출력

######
	select * 
	from
	( select * from files 
	where 
	(id, product_id ) 
	in 
	( select min(id) as id, product_id from files group by product_id ) 
	order by id desc ) 
	files 
	group by files.product_id 
		
	
	
- 서브쿼리

######

	서브쿼리 -> 메인쿼리 순
	스칼라 서브쿼리 : SELECT문에 사용, 컬럼처럼 사용, 하나의 결과()만 나오도록 작성
	인라인 뷰 : FROM절에 사용, 테이블처럼 사용, 반드시 별칭을 지정해줘야한다
	서브쿼리 : WHERE절에 사용, 변수처럼 사용
	
	
- 프로그래머스 Lv2 자동차 평균 대여 기간 구하기
	->CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블에서 평균 대여 기간이 7일 이상인 자동차들의 자동차 ID와 평균 대여 기간(컬럼명: AVERAGE_DURATION) 리스트를 출력하는 SQL문을 작		성해주세요. 평균 대여 기간은 소수점 두번째 자리에서 반올림하고, 결과는 평균 대여 기간을 기준으로 내림차순 정렬해주시고, 평균 대여 기간이 같으면 자동차 ID를 기준으로 		내림차순 정렬해주세요.
	
######

	SELECT CAR_ID, ROUND(AVG(DATEDIFF(END_DATE, START_DATE)) + 1, 1) AS AVERAGE_DURATION
	FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
	GROUP BY CAR_ID
	HAVING AVERAGE_DURATION >= 7 
	ORDER BY AVERAGE_DURATION DESC, CAR_ID DESC
	
	
- 프로그래머스 Lv2 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기
	->CAR_RENTAL_COMPANY_CAR 테이블에서 '통풍시트', '열선시트', '가죽시트' 중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지 출력하는 SQL문을 작성해주세요. 이		때 자동차 수에 대한 컬럼명은 CARS로 지정하고, 결과는 자동차 종류를 기준으로 오름차순 정렬해주세요.

######

	SELECT CAR_TYPE, COUNT(*) AS CARS 
	FROM CAR_RENTAL_COMPANY_CAR
	WHERE OPTIONS LIKE "%시트%"
	GROUP BY CAR_TYPE
	ORDER BY CAR_TYPE ASC
	
	
- 프로그래머스 Lv3 오랜 기간 보호한 동물(1)
	->아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일 순으로 조회해야 합니다.

######
	
	SELECT ANIMAL_INS.NAME, ANIMAL_INS.DATETIME 
	FROM ANIMAL_INS
	LEFT JOIN ANIMAL_OUTS 
	ON ANIMAL_INS.ANIMAL_ID = ANIMAL_OUTS.ANIMAL_ID
	WHERE ANIMAL_OUTS.ANIMAL_ID IS NULL
	ORDER BY ANIMIAL_INS.DATETIME ASC
	LIMIT 3

