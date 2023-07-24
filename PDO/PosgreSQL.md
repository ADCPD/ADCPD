### FILTER IN DATESTAMP 

1. Use ``BETWEEN``

```SQL
SELECT contract_id, garbage_truck_code,  garbage_collection_planed_id,  SUM(effectiv) / SUM(attemped) * 100 AS rate_correspondance, ROUND(100 - (SUM(effectiv) / SUM(attemped) * 100), 2) AS rate_of_non_correspondance
FROM rate_of_collection_by_truck 
WHERE contract_id = '6025939f-5574-4b31-9318-779c3f44bae6' 
AND time BETWEEN '2023-07-19' AND '2023-07-19 23:59:59' 
AND garbage_collection_planed_id IN ('165847f3-be4f-467f-b650-88496eb2c23d','9abef47f-5e68-4449-b53a-04fa6de07d93','9fab297e-26e0-483f-8c2a-2a1e8ceca44b')  
GROUP BY contract_id, garbage_collection_planed_id, garbage_truck_code 
```

2. Use ``CAST``

```SQL
SELECT DISTINCT
rgcp.id AS collection_planned_id, rgcp."label", rgcp.code, rgcp.trash_flow, rgcp.created_at, rgcp.updated_at, rgcp.contract_id, rgcp.date_last_update , rgcp.provider
FROM  ref_garbage_collection_planed rgcp  
INNER JOIN ref_collection_meta_data rcmd ON rgcp.id = rcmd.garbage_collection_planed_id
WHERE rgcp.contract_id = '6025939f-5574-4b31-9318-779c3f44bae6' 
AND (CAST(rgcp.created_at AS VARCHAR) LIKE '2023-07-19 %')
``` 
