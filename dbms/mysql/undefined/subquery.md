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
```
