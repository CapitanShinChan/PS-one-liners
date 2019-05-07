# PS-one-liners
Simple but usefull Powershell one-line commands for daily tasks

* Get ip addresses from a file (one per line), remove duplicates and order them ascending
```Powershell
  gc .\ips.txt | sort -Unique | %{[System.Net.IPAddress]::Parse($_)} | sort {$bytes=$_.GetAddressBytes();[array]::Reverse($bytes);[BitConverter]::ToUInt32($bytes,0)} | ft IPAddressToString
```

* Download a file to disk through HTTP
```Powershell
Invoke-WebRequest -Uri "https://file.com/file.txt" -OutFile "C:\file.txt"
Start-BitsTransfer -Source "https://file.com/file.txt" -Destination ".\file.txt"
```

* Process a file line by line and do any operation
```Powershell
foreach ($line in [System.IO.File]::ReadLines($file)) { Resolve-DnsName $line | select Name,IP4Address}
```

* Read file as bytes and convert it to base64
```Powershell
[System.Convert]::ToBase64String($(gc .\olakase.exe -Encoding Byte))
```
* Write base64 string as a binary file
```Powershell
Set-Content -Path .\are_you_Rick_Sanchez.exe -Value $([System.Convert]::FromBase64String($b64)) -Encoding Byte
```

* List all listening ports in the local machine and get the process name associated to them
```Powershell
Get-NetTCPConnection | Where {$_.State -eq "Listen"} | Select local*,state,@{Name="Process";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}},@{Name="Description";Expression={(Get-Process -Id $_.OwningProcess).Description}}| sort -Property LocalAddress | ft -AutoSize
```


## Gathering info about AD, users, groups, sessions, shares, etc...
* List all users logged on the current machine
```Powershell
$(Get-CimInstance Win32_LoggedOnUser).antecedent.name | Select-Object -Unique
```
