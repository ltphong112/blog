---
title: "Install Windows Update From Powershell"
date: 2022-12-15T08:12:43-08:00
---

This guide will show how to install Windows updates from Powershell.
Make sure the Execution Policies are allowed with this command

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Or

```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
```

Install Windows Updates module via Powershell

```
Install-Module PSWindowsUpdate
```

Retrive list of updates

```
Get-WindowsUpdate
```

Install all the updates

```
Install-WindowsUpdate
```

Automation the installation and reboot, log file with:

```
Install-WindowsUpdate -MicrosoftUpdate -AcceptAll -AutoReboot | Out-File "C:\($env.computername-Get-Date -f yyyy-MM-dd)-MSUpdates.log" -Force
```
