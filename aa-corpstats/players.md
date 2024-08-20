## Characters with missing ESI keys
Checks with characters don't have their ESI keys on auth so your diplos can hunt them down:

```
SELECT mainchar.character_name AS "Main Character Name", evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker"
FROM alliance_auth.eveonline_evecharacter evechar
JOIN alliance_auth.corptools_characteraudit charaudit ON evechar.id != charaudit.id OR evechar.id = charaudit.id AND charaudit.active = 0
JOIN alliance_auth.authentication_characterownership charowner ON evechar.id = charowner.character_id
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter mainchar ON userprofile.main_character_id = mainchar.id
WHERE evechar.alliance_name = "Shadow Ultimatum"
```

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