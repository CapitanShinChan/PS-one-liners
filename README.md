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

* Read file as bytes and convert it to base64
```Powershell
[System.Convert]::ToBase64String($(gc .\olakase.exe -Encoding Byte))
```
