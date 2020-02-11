Managing processes running inside a container or on virtual machine is a common requirement for systems automation. PowerShell makes process management very easy, with a set of built-in commands, no installation of third-party modules needed.

```powershell
Get-Command -Name *process*
```

If you have other PowerShell modules installed on your system, you might get more results than expected, using the above command. To retrieve only the process management commands built into PowerShell, use this command instead.

```powershell
Get-Command -Name *process* -Module Microsoft.PowerShell*
```

### Starting a Process

You can launch new process synchronously or asynchronously by using the `Start-Process` command.

```powershell
Start-Process -FilePath ls
```

You can also pass command line arguments to the process that you're launching, using the `-ArgumentList` parameter.

```powershell
Start-Process -FilePath ls -ArgumentList '-lGa' -Wait
```

By default, the `Start-Process` command will return you to an interactive shell, before the specified process is finished running. This default behavior is known as asynchronous process creation. If you would like `Start-Process` to be synchronous instead, use the `-Wait` parameter.

```powershell
Start-Process -FilePath sleep -ArgumentList 3 -Wait
```

You might have noticed that the `Start-Process` command is emitting `stdout` output from external commands, but it doesn't return any PowerShell objects. You can grab a reference to the process by specifying the `-PassThru` parameter, and preceding the invocation with a variable assignment.

```powershell
$MyProcess = Start-Process -FilePath sleep -ArgumentList 10 -PassThru
```

### Killing a Process

To stop or kill a process, use the `Stop-Process` command. The following example will kill the current PowerShell session, using the automatic `$PID` variable. After killing PowerShell, just restart it by running `pwsh`.

```powershell
Stop-Process -Id $PID
```

If you'd rather specify a process name to kill, instead of a specific process ID, you can use the `-Name` parameter. If there are multiple processes with the specified name, they will all be killed.

```
Stop-Process -Name pwsh
```