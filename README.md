# MySQL 정리

## DISTINCT는 중복제거를 해준다.
```
SELECT DISTINCT 컬럼명 
FROM 테이블명;
```

## BINARY는 대소문자를 구별하게 해준다.
```
SELECT * 
FROM 테이블명 
where BINARY(컬럼명) in ('컬럼내용');
```
## CONCAT은 데이터와 문자도 합칠수있다.
```
UPDATE 테이블명 컬럼명 = CONCAT(컬럼명, ', Update')
WHERE 조건;
```
## CASE문은 조건에 따라서 값을 지정해 준다.
```
CASE
WHEN 조건1 THEN 값1 
WHEN 조건2 THEN 값2 
ELSE 값3
END
```
```
# UPDATE CASE WHEN
UPDATE recursive_test_table
  SET parent_id = CASE 
      WHEN parent_id = 1 THEN 10
      WHEN parent_id = 2 THEN 20
      WHEN parent_id = 3 THEN 30
      WHEN parent_id = 6 THEN 60
      ELSE parent_id
      END;
```
## OUTER JOIN
- 기준 테이블에만 데이터가 존재하면 조회된다.
- 조건에 부합하지 않는 행까지 포함시켜 결합한다.
- 기본적으로 left, right, full이 outer join이다.

## LEFT JOIN
- 왼쪽 테이블을 중심으로 오른쪽의 테이블을 매치시킨다.
- 왼쪽 테이블의 한개의 레코드에 여러개의 오른쪽 테이블 레코드가 일치할 경우, 해당 왼쪽 레코드를 여러번 표시하게 된다.
- 왼쪽은 무조건 표시하고, 매치되는 레코드가 오른쪽에 없으면 null을 표시한다.
```
SELECT *
FROM 테이블명 A
LEFT JOIN 테이블명 B ON B.컬러명 = A.컬럼명
WHERE B.컬럼명 IS NULL
```

## INNER JOIN은 교집합, 기준 테이블과 조인 테이블 모두 데이터가 존재해야 조회된다.
### GROUP BY는 특정 컬럼을 그룹화 한다. 사용시 주의점으로는 select에서 사용한 컬럼들은 group by에서 그래도 써주어야함.
### WHERE는 그룹화 전 조건이다.
### HAVING은 그룹화 후 조건이다.
### ORDER BY는 오름차순, 내림차순을 결정해준다. select문 맨 마지막에 위치한다. ASC 오름차순(디폴트), DESC 내림차순
```
SELECT T2.컬럼명, T2.컬럼명
FROM (
SELECT T2.컬럼명, T2.컬럼명
FROM 테이블명
WHERE 조건
GROUP BY T2.컬럼명, T2.컬럼명
HAVING 조건
) T1
INNER JOIN 테이블명 T2 ON 조인될 조건 AND 조인될 조건
ORDER BY KIND
;
```

## exists는 ()안에 서브쿼리만 올 수 있다.
- in은 ()안에 특정값이나, 서브쿼리가 올 수 있다.
- exists가 성능은 더 좋다.
```
SELECT * 
FROM 테이블명
WHERE EXISTS 
( 
SELECT * 
FROM 테이블명 
WHERE 컬럼명 = 컬럼명
)
;
```

## UNION
- 두개의 select 결과를 합칠수 있다. 합친 결과에서 중복되는 행은 하나만 표시한다.
- union all은 중복제거를 하지 않고 모두 합쳐서 보여준다.
```
SELECT * 
FROM A
UNION  (ALL)      
SELECT * 
FROM B
```

같지않음을 표현하는 연산자
```
!=
^=
<>
```

## LPAD, RPAD 함수
- LPAD는 지정한 길이 만큼 왼쪽부터 특정문자로 채워준다
- LPAD('값', '총 문자길이', '채움문자')
- RPAD는 오른쪽을 특정문자로 채워준다
```
사용법 : LPAD(원본문자열 , 원하는 자리수, 채울 문자열)
ex ) SELECT LPAD('ABC',10,'0')  FROM 테이블명;
결과 : 0000000ABC

사용법 : RPAD(원본문자열 , 원하는 자리수, 채울 문자열)
ex ) SELECT RPAD('ABC',10,'0')  FROM 테이블명;
결과 : ABC0000000
```


## 문자열 자르기
- Left함수는 문자열을 받아서 왼쪽부터 원하는 길이만큼 자르는 함수이다.
- LEFT(문자열,길이)

- RIGHT함수는 문자열을 받아서 오른쪽부터 원하는 길이만큼 자르는 함수이다.
- RIGHT(문자열,길이)

- SubString함수의 기능은 문자열을 받아서 일정한 영역만큼 잘라낸 후 리턴하는 기능을 가지고 있습니다.
- SUBSTRING(문자열,시작자리번호,자를문자수)

## IFNULL
- 해당 컬럼의 값이 NULL울 반환할 때, 다른 값으로 출력할 수 있도록 하는 함수이다.
```
// 컬럼명의 값이 NULL일 경우 대체 값 출력
SELECT IFNULL(컬럼명, "Null일 경우 대체 값") FROM 테이블명; 
```

## EXPLAIN
- 쿼리문 맨 위에 EXPLAIN 입력
- 쿼리문에 대한 설명이 나와있음
- EXPLAIN를 사용함으로써, 테이블의 어느 곳에 인덱스를 추가해야만 열을 찾기 위한 SELECT가 보다 빠르게 되는지를 알 수 있게 된다.
- EXPLAIN를 사용하면 옵티마이저가 최적의 (optimal) 순서로 테이블을 조인 (join)할 수 있는지 여부도 검사할 수가 있다.



