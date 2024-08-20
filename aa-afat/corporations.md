## FATs in relation to their corp size
Calculates how many FATs each character inside a corp has and how many percentage of people do PvP with at least 4 FATs per player:

```
SELECT 
    evechar.corporation_name AS "Corporation Name", 
    evechar.corporation_ticker AS "Corporation Ticker", 
    evechar.alliance_name AS "Alliance Name", 
    evechar.alliance_ticker AS "Alliance Ticker", 
    COUNT(fat.id) AS FATs,
    COALESCE(player_counts.actual_players, 0) AS "Actual Players",
    COALESCE(COUNT(fat.id) / NULLIF(player_counts.actual_players, 0), 0) AS "FATs per Player",
    (COALESCE(COUNT(fat.id), 0) / (COALESCE(player_counts.actual_players, 0) * 4)) * 100 AS "Effectiveness (%)"
FROM 
    alliance_auth.afat_fat fat 
JOIN 
    alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN 
    alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN 
    alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN 
    alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
LEFT JOIN 
    (SELECT 
        evechar.corporation_name, 
        evechar.corporation_ticker, 
        COUNT(evechar.character_name) AS actual_players
     FROM 
        alliance_auth.authentication_userprofile userprofile
     JOIN 
        alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
     GROUP BY 
        evechar.corporation_name, evechar.corporation_ticker
    ) AS player_counts 
ON 
    evechar.corporation_name = player_counts.corporation_name
    AND evechar.corporation_ticker = player_counts.corporation_ticker
GROUP BY 
    evechar.corporation_name, evechar.corporation_ticker
ORDER BY 
    FATs DESC;
```

## Top Monthly Corporations
Calculates how many FATs each character inside a corp has and adds them together:

```
SELECT evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
GROUP BY evechar.corporation_name
ORDER BY FATs DESC
```