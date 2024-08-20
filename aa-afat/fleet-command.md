## Monthly Top Fleet Commanders
Goes through all created fatlinks, groups them together and displays how many were created by one FC:

```
SELECT 
  evechar.character_name AS "Fleet Commander", 
  evechar.corporation_name AS "Corporation Name", 
  evechar.corporation_ticker AS "Corporation Ticker", 
  evechar.alliance_name AS "Alliance Name", 
  evechar.alliance_ticker AS "Alliance Ticker", 
  COUNT(fatlink.id) AS "Created FAT Links"
FROM alliance_auth.afat_fatlink fatlink
JOIN alliance_auth.authentication_userprofile userprofile ON fatlink.creator_id = userprofile.id 
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id 
WHERE $__timeFilter(fatlink.created)
GROUP BY fatlink.creator_id
```