# Web Jam!

New skills during Web Jam:

## Directory fuzzing

`dirb http://<web_url> /usr/share/wordlists/dirb/common.txt`

(this might take a while)


## Cracking JWT cookies

- Go to jwt.io and plug in that cookie to see what those fields are!
- Downloaded jwt_tool (see [hacktricks](https://book.hacktricks.xyz/pentesting-web/hacking-jwt-json-web-tokens))
- Crack an HS256 key: `python3 jwt_tool <JWT> -C -d /usr/share/wordlists/rockyou.txt` (this might take a while)
- Tamper with cookie: `python3 jwt_tool <JWT> -S hs256 -p "<cracked_key>" -I -hc <claim> -pv <value>`

Then feed the website with the tampered cookie
