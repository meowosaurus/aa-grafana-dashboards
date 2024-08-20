## Corporation Missing ESI Keys Effectiveness
Checks how many characters of a corp don't have ESI keys available and gives you the percentage of how many chars are authed:

```
WITH MissingESI AS (
    SELECT evechar.corporation_name, COUNT(evechar.character_name) AS missing_count
    FROM alliance_auth.eveonline_evecharacter evechar 
    JOIN alliance_auth.corptools_characteraudit charaudit 
    ON evechar.id != charaudit.character_id OR evechar.id = charaudit.character_id AND charaudit.active = 0
    WHERE alliance_name = "Shadow Ultimatum"
    GROUP BY evechar.corporation_name
)
SELECT 
    evechar.corporation_name AS "Corporation Name", 
    evechar.alliance_name AS "Alliance Name", 
    COUNT(DISTINCT evechar.character_name) AS "Total Characters In Corp", 
    m.missing_count AS "ESI Keys Missing",
    (1 - (m.missing_count / COUNT(DISTINCT evechar.character_name))) * 100 AS "Effectiveness (%)"
FROM alliance_auth.eveonline_evecharacter evechar
JOIN MissingESI m
ON evechar.corporation_name = m.corporation_name
WHERE alliance_name = "Shadow Ultimatum"
GROUP BY evechar.corporation_name
```