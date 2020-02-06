Now that you have a functioning PowerShell environment, let's explore what you can do.

PowerShell has a few "essential" commands to remember, which help you to explore the PowerShell environment.

* `Get-Command` discovers a list of available commands in the environment.
* `Get-Help` shows you how to call any PowerShell command.
* `Get-Module` shows you a list of modules that are currently imported into the environment.
* `Get-Member` shows you a list of properties, methods, and events on any object.

### Finding PowerShell Commands

Where do you start in PowerShell? First, you need to find a command to retrieve or manipulate information.

Start by running `Get-Command` and examining the output. You'll notice that you receive a large list of commands displayed in a column-based format. The columns represent:

1. Command type (cmdlet, function, etc.)
1. Name of the command
1. Version of the module that contains the command
1. Module name, that contains the command

If you want to obtain a simple count of how many commands are available in the environment, you can wrap the array output in parentheses and examine the `Count` property.

```
(Get-Command).Count
```

That's a lot of commands! How do you filter this down to something more manageable?

You can specify the `-Name` parameter, and use wildcards (asterisks) to find commands matching a particular name.

```powershell
Get-Command -Name *location*
```

### Exploring PowerShell Modules

To explore all of the PowerShell modules installed on the system, use this command.

```powershell
Get-Module -ListAvailable
```

Not all of the _installed_ PowerShell modules are _imported_ by default; there's a distinction. To view a list of only the currently _imported_ modules, try this.

```powershell
Get-Module
```

To retrieve the list of commands that are exported (exposed) by a particular module, try this.

```powershell
Get-Command -Module Microsoft.PowerShell.Management
```