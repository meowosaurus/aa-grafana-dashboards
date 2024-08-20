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
