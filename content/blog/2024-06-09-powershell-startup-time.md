---
id: powershell-startup-time
tags: 
title: 🐚 powershell startup time
modified: 2025-05-18T09:12:05-07:00
created: 024-06-09T16:59:33-07:00
---

# 🐚 PowerShell Startup Time

I noticed that [PowerShell](PowerShell.md) was taking a long time to start. One common tip is to launch it with the `-nologo`:

```
pwsh -nologo
```

However, this didn't make a noticeable difference.

While searching for solutions, I came across this Stack Overflow post:  
[PowerShell steps to fix slow startup](https://stackoverflow.com/questions/59341482/powershell-steps-to-fix-slow-startup)

The post suggests pre-compiling loaded assemblies using `ngen.exe`. Here’s the script it recommends (to be run as Administrator):

```powershell
$env:PATH = [Runtime.InteropServices.RuntimeEnvironment]::GetRuntimeDirectory()
[AppDomain]::CurrentDomain.GetAssemblies() | ForEach-Object {
    $path = $_.Location
    if ($path) {
        $name = Split-Path $path -Leaf
        Write-Host -ForegroundColor Yellow "`r`nRunning ngen.exe on '$name'"
        ngen.exe install $path /nologo
    }
}
```

When I tried this, I got an error saying `ngen.exe` was not found. It turns out `ngen.exe` is included with Visual Studio. So I launched a _Developer PowerShell_ from Visual Studio and ran the script there.

After doing this, PowerShell startup (especially with `-nologo`) became noticeably faster.
