## Monthly Top Fleet Commanders

```
SELECT evechar.character_name AS "Fleet Commander", COUNT(fatlink.id) AS "Created FATs"
FROM alliance_auth.afat_fatlink fatlink
JOIN alliance_auth.authentication_userprofile userprofile ON fatlink.creator_id = userprofile.id 
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id 
GROUP BY fatlink.creator_id
```