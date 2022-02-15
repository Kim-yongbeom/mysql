## binary는 대소문자를 구별하게 해준다.
```
SELECT * FROM 테이블명 where BINARY(컬럼명) in ('컬럼내용');
```

## concat은 데이터와 문자도 합칠수있다.
```
UPDATE 테이블명 컬럼명 = CONCAT(컬럼명, ', Update') WHERE 조건;
```

## case문은 조건에 따라서 값을 지정해 준다.
```
CASE
WHEN 조건1 THEN 값1 
WHEN 조건2 THEN 값2 
ELSE 값3
END
```
## inner join은 교집합, 기준 테이블과 조인 테이블 모두 데이터가 존재해야 조회된다.
```
SELECT T2.컬럼명
FROM (
SELECT 여러 컬럼들
FROM 테이블명
WHERE 조건

# 여기부터!!

 GROUP BY 여러 컬럼들
 HAVING COUNT(*) > 1
) T1
INNER JOIN tmp_node_mst_v230 T2 ON T2.KIND = T1.KIND
ORDER BY KIND
;
```
## outer join은 기준 테이블에만 데이터가 존재하면 조회된다.
