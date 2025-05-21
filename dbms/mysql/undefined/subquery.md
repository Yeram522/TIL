# SUBQUERY

```sql
-- 1. 부서코드가 노옹철 사원과 같은 소속의 직원 명단 조회하세요.
SELECT
       DEPT_CODE 부서코드
	,  EMP_NAME 직원이름
  FROM EMPLOYEE
 WHERE DEPT_CODE = (SELECT
						   DEPT_CODE
					  FROM EMPLOYEE
                      WHERE EMP_NAME = '노옹철');
                      
-- 2. 전 직원의 평균 급여보다 많은 급여를 받고 있는 직원의 사번, 이름, 직급코드, 급여를 조회하세요.
SELECT
       EMP_NO
	,  EMP_NAME
    ,  JOB_CODE
    ,  SALARY
 FROM EMPLOYEE
WHERE SALARY > (SELECT
						 AVG(SALARY)
					FROM EMPLOYEE);
                        
-- 3. 노옹철 사원의 급여보다 많이 받는 직원의 사번, 이름, 부서코드, 직급코드, 급여를 조회하세요.
SELECT
       EMP_NO
	,  EMP_NAME
    ,  JOB_CODE
    ,  SALARY
 FROM EMPLOYEE
WHERE SALARY > (SELECT
					   SALARY
				  FROM EMPLOYEE
				 WHERE EMP_NAME = '노옹철');
                    
-- 4. 가장 적은 급여를 받는 직원의 사번, 이름, 부서코드, 직급코드, 급여, 입사일을 조회하세요.
SELECT
       EMP_NO
     , EMP_NAME
     , DEPT_CODE
     , JOB_CODE
     , SALARY
     , HIRE_DATE
 FROM EMPLOYEE
 ORDER BY SALARY ASC
 LIMIT 1; -- 오름차순 정렬 후 상위 첫번째 행 조회
 
-- *** 서브쿼리는 SELECT, FROM, WHERE, HAVING, ORDER BY절에도 사용할 수 있다.

-- 5. 부서별 최고 급여를 받는 직원의 이름, 직급코드, 부서코드, 급여 조회하세요.
-- 먼저 부서별로 GROUP BY 해서 ORDER DESC 해서 첫번째 애들만 가져오기.

SELECT
       DEPT_CODE
	 , MAX(SALARY)
  FROM EMPLOYEE
 GROUP BY DEPT_CODE;
	
SELECT
       A.EMP_NAME
	,  A.JOB_CODE
    ,  A.DEPT_CODE
    ,  A.SALARY
 FROM EMPLOYEE A
 JOIN (SELECT
	         DEPT_CODE
		   , MAX(SALARY) salary
        FROM EMPLOYEE
	  GROUP BY DEPT_CODE) B ON A.SALARY = B.salary ;

-- *** 여기서부터 난이도 극상

-- 6. 관리자에 해당하는 직원에 대한 정보와 관리자가 아닌 직원의 정보를 추출하여 조회하세요.
-- 사번, 이름, 부서명, 직급, '관리자' AS 구분 / '직원' AS 구분
-- HINT!! is not null, union(혹은 then, else), distinct
-- 부서가 없는 경우에는 inner join을 하면 결과가 나오지 않으므로 left join을 이용해서, employee의 부서가 null이어도 반영될 수 있게 해아한다!!
SELECT
      emp.EMP_NO 사번
	, emp.EMP_NAME 이름
    , depart.DEPT_TITLE 부서명
    , jb.JOB_NAME 직급
    , '관리자' 구분
 FROM EMPLOYEE emp
 LEFT JOIN DEPARTMENT depart ON emp.DEPT_CODE = depart.DEPT_ID 
 JOIN JOB jb Using(JOB_CODE)
 WHERE emp.MANAGER_ID IS NULL
 UNION
 SELECT
      emp.EMP_NO 사번
	, emp.EMP_NAME 이름
    , depart.DEPT_TITLE 부서명
    , jb.JOB_NAME 직급
    , '직원' 구분
 FROM EMPLOYEE emp
 LEFT JOIN DEPARTMENT depart ON emp.DEPT_CODE = depart.DEPT_ID
 JOIN JOB jb Using(JOB_CODE)
 WHERE emp.MANAGER_ID IS NOT NULL;

-- 7. 자기 직급의 평균 급여를 받고 있는 직원의 사번, 이름, 직급코드, 급여를 조회하세요.
-- 단, 급여와 급여 평균은 만원단위로 계산하세요.
-- HINT!! round(컬럼명, -5)
SELECT
       A.EMP_NO
	 , A.EMP_NAME
	 , A.JOB_CODE
     , A.SALARY
 FROM EMPLOYEE A
 JOIN (SELECT
			  AVG(SALARY) avg
			  FROM EMPLOYEE
			 GROUP BY DEPT_CODE) B ON  round(A.SALARY, -5) = round(B.avg, -5);

-- 8. 퇴사한 여직원과 같은 부서, 같은 직급에 해당하는 직원의 이름, 직급코드, 부서코드, 입사일을 조회하세요.
SELECT
       A.EMP_NAME
	,  A.JOB_CODE
    ,  A.DEPT_CODE
    ,  A.HIRE_DATE
 FROM  EMPLOYEE A
 JOIN (SELECT
			  B.DEPT_CODE
			, B.JOB_CODE
		 FROM EMPLOYEE B
         WHERE B.ENT_YN = 'Y') C ON (A.JOB_CODE = C.JOB_CODE AND A.DEPT_CODE = C.DEPT_CODE);
         
-- 9. 급여 평균 3위 안에 드는 부서의 부서 코드와 부서명, 평균급여를 조회하세요.
-- HINT!! limit
--  평균 3위안에 드는 부서? 같은 부서끼리의 SALARY 평균을 ORDER BY ( 서브쿼리 먼저 작성 )
SELECT
       DEPT_CODE
	,  AVG(SALARY) avg_sal
 FROM EMPLOYEE 
 GROUP BY DEPT_CODE
 ORDER BY avg_sal DESC
 LIMIT 3;
 
SELECT
       DEPT_CODE
	,  depart.DEPT_TITLE
    ,  emp.avg_sal
 FROM  (SELECT
              DEPT_CODE
	       ,  AVG(SALARY) avg_sal
         FROM EMPLOYEE 
		GROUP BY DEPT_CODE
		ORDER BY avg_sal DESC
		LIMIT 3) emp
 JOIN DEPARTMENT depart ON emp.DEPT_CODE = depart.DEPT_ID;

-- 10. 부서별 급여 합계가 전체 급여의 총 합의 20%보다 많은 부서의 부서명과, 부서별 급여 합계를 조회하세요.
-- 부서별 급여 합계 구하기 서브쿼리
SELECT
       DEPT_CODE
	,  SUM(SALARY)
  FROM EMPLOYEE
 GROUP BY DEPT_CODE;
 
 -- 전체 급여의 총 합 서브쿼리
 SELECT
        SUM(SALARY)
  FROM EMPLOYEE;
  
SELECT
       depart.DEPT_TITLE
	,  sum_salary.dept_sal
  FROM (SELECT
            DEPT_CODE
	     ,  SUM(SALARY) dept_sal
		 FROM EMPLOYEE
        GROUP BY DEPT_CODE) sum_salary
  JOIN DEPARTMENT depart ON sum_salary.DEPT_CODE = depart.DEPT_ID
  WHERE sum_salary.dept_sal > ( SELECT
									   SUM(SALARY)
								  FROM EMPLOYEE)*(20/100);
```
