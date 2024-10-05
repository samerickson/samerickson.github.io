---
id: powershell-startup-time
tags: []
title: 🐚 powershell startup time
---

# 🐚 PowerShell Startup Time

I recently found that my startup time for [powershell](powershell.md) has been really slow. To combat this I found some resources indicating that launching [powershell](powershell.md) with `-nologo` to speed things up. However I was not seeing the results that I wanted. That is when I found this page [PowerShell steps to fix slow startup](https://stackoverflow.com/questions/59341482/powershell-steps-to-fix-slow-startup).

That link suggests running the following as administrator:

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

When I tried it I got an error indicating that `ngen.exe` could not be found. I did some digging and discovered that this is automatically installed with Visual Studio. So I opened Visual Studio and got a Developer PowerShell then ran the script.

After doing this the start up time of pwsh (with `-nologo`) was significantly improved.
