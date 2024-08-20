# Alliance Auth Another Fleet Activity Tracking

## Monthly FATs
All FATs by characters are getting grouped by their account owner (player) and displayed:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
GROUP BY evechar.character_name
ORDER BY FATs DESC
```

## Player Minimum FATs
Goes through all players, groups their characters together and checks if they combined have at least 4 FATs:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
GROUP BY evechar.character_name
HAVING FATs < 4
ORDER BY FATs DESC
```

## Raw Tackle Participation
Goes through all players, groups their characters together and checks if they flew a tackle ship:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
WHERE fat.shiptype IN ('Slasher', 'Rifter', 'Stiletto', 'Sabre', 'Condor', 'Merlin', 'Crow', 'Flycatcher', 'Atron', 'Incursus', 'Maulus Navy Issue', 'Ares', 'Keres', 'Eris', 'Punisher', 'Executioner', 'Malediction', 'Heretic')
GROUP BY evechar.character_name
ORDER BY FATs DESC
```

## Raw Logi Participation
Goes through all players, groups their characters together and checks if they flew a logi ship:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
WHERE fat.shiptype IN ('Inquisitor', 'Deacon', 'Augoror', 'Guardian', 'Bantam', 'Kirin', 'Burst', 'Scalpel', 'Scythe', 'Osprey', 'Scimitar', 'Basilisk', 'Navitas', 'Thalia', 'Exequror', 'Oneiros')
GROUP BY evechar.character_name
ORDER BY FATs DESC
```

## Raw Boost Participation
Goes through all players, groups their characters together and checks if they flew a boost ship:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
WHERE fat.shiptype IN ('Bifrost', 'Stork', 'Magus', 'Pontifex', 'Claymore', 'Vulture', 'Damnation', 'Eos')
GROUP BY evechar.character_name
ORDER BY FATs DESC
```

## Raw EWAR Participation
Goes through all players, groups their characters together and checks if they flew an EWAR ship:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
WHERE fat.shiptype IN ('Vigil', 'Vigil Fleet Issue', 'Hyena', 'Huginn', 'Maulus', 'Griffin', 'Griffin Navy Issue', 'Kitsune', 'Rook', 'Blackbird', 'Celestis', 'Bellicose', 'Crucifier', 'Crucifier Navy Issue', 'Sentinel', 'Curse', 'Arbitrator')
GROUP BY evechar.character_name
ORDER BY FATs DESC
```

## Raw Special Snowflakes Participation
Goes through all players, groups their characters together and checks if they flew an special snowflakes ship:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
WHERE fat.shiptype IN ('Onyx', 'Broadsword', 'Phobos', 'Devoter')
GROUP BY evechar.character_name
ORDER BY FATs DESC
```

## Raw (Super-)Capital Participation
Goes through all players, groups their characters together and checks if they flew a (super-)capital ship:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
WHERE fat.shiptype IN ('Revelation', 'Revelation Navy Issue', 'Bane', 'Apostile', 'Aeon', 'Archon', 'Naglfar', 'Naglfar Fleet Issue', 'Valravn', 'Lif', 'Nidhoggur', 'Hel', 'Moros', 'Moros Navy Issue', 'Hubris', 'Ninazu', 'Thanatos', 'Nyx', 'Phoenix', 'Phoenix Navy Issue', 'Karura', 'Minokawa', 'Wyvern', 'Chimera')
GROUP BY evechar.character_name
ORDER BY FATs DESC
```

## Raw Titan Participation
Goes through all players, groups their characters together and checks if they flew a titan ship:

```
SELECT evechar.character_name AS "Character Name", evechar.corporation_name AS "Corporation Name", evechar.corporation_ticker AS "Corporation Ticker", evechar.alliance_name AS "Alliance Name", evechar.alliance_ticker AS "Alliance Ticker", COUNT(fat.id) AS FATs
FROM alliance_auth.afat_fat fat 
JOIN alliance_auth.afat_fatlink fatlink ON fat.fatlink_id = fatlink.id
JOIN alliance_auth.authentication_characterownership charowner ON fat.character_id = charowner.character_id 
JOIN alliance_auth.authentication_userprofile userprofile ON charowner.user_id = userprofile.id
JOIN alliance_auth.eveonline_evecharacter evechar ON userprofile.main_character_id = evechar.id
WHERE fat.shiptype IN ('Avatar', 'Levithan', 'Ragnarok', 'Erebus')
GROUP BY evechar.character_name
ORDER BY FATs DESC
```