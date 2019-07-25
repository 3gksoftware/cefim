Welcome to the cefim wiki!


# cefim
Formation CEFIM





## Création de la vue pour récupérer les matchs


```
CREATE OR REPLACE VIEW vw_m AS  SELECT
    m.id AS m1,
    m.displayname AS p1,
    mm.id AS m2,
    mm.displayname AS p2,
    ma.dating_date AS dating_date
FROM
    (
        (
            dating_member_match ma
        JOIN dating_member m ON
            (m.id = ma.dating_member_id)
        )
    JOIN dating_member mm ON
        (
            mm.id = ma.match_dating_member_id
        )
)
```
## Requête simple de récupération des personnes ayant matchées

```
SELECT v1.m1,v1.m2 from  vw_m as v1 INNER JOIN vw_m as v2 ON v1.m1=v2.m2 AND v1.m2=v2.m1
```

## Requête améliorée de récupération des personnes ayant matchées

```
SELECT DISTINCT
	CASE WHEN v1.m1>	v1.m2 THEN v1.m1 ELSE v1.m2 END,
	CASE WHEN v1.m1>	v1.m2 THEN v1.m2 ELSE v1.m1 END
	FROM  
	vw_m as v1 
	INNER JOIN vw_m as v2 ON v1.m1=v2.m2 AND v1.m2=v2.m1
```
