## Actual Corporation Players
```
SELECT evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", COUNT(evechar.character_name) AS "Actual Players"
FROM alliance_auth.authentication_userprofile userprofile
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
GROUP BY evechar.corporation_name
```