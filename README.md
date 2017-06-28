# PS-one-liners
Simple but usefull Powershell one-line commands for daily tasks

* Get ip addresses from a file (one per line), remove duplicates and order them ascending
```Powershell
  gc .\ips.txt | sort -Unique | %{[System.Net.IPAddress]::Parse($_)} | sort {$bytes=$_.GetAddressBytes();[array]::Reverse($bytes);[BitConverter]::ToUInt32($bytes,0)} | ft IPAddressToString
```
