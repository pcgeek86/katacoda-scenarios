By default, [PowerShell variables](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_variables?view=powershell-7) are dynamically typed. You can optionally assign static types to variables at declaration time.

### Dynamic Typing

For starters, let's look at a simple example of dynamic typing. You can assign a string value to a variable, and later change it to an integer.

```
$Text = 'Hello PowerShell'
$Text = 5
```

### Static Typing

If you want to create a statically-typed variable, you can specify the data type preceding the variable name. To denote the data type, use square brackets, and specify the .NET type that the variable should point to.

```
[int] $MyInteger = 5
[System.Diagnostics.Process] $Process = Get-Process -Id $PID

$MyInteger = 'Hello PowerShell'
$Process = 5
```

### PowerShell Type Casting

Take note that PowerShell will automatically try to convert values to different types, in some cases. For example, if you declare a variable as a `[string]` type, PowerShell will still allow you to assign an `[int]` value of `5` to it. However, before assignment, PowerShell will convert the integer value to a string value.

In the following example, you'll notice that, even though we assign an `[int]` value to a `[string]` variable, the variable's type is still `[string]`. The [`GetType()` method](https://docs.microsoft.com/en-us/dotnet/api/system.object.gettype?view=netcore-3.1) is defined on the `System.Object` class, and is therefore available on all .NET objects. You can use this method to inspect the data type of nearly any object in PowerShell.

```
[string] $MyString = 'PowerShell'
$MyString = 5
$MyString.GetType()
```

### Variable Management Commands

PowerShell provides several native commands, in the `Microsoft.PowerShell.Utility` module, that allow you to create and manage variables. To discover the variable management commands in PowerShell, run the following command.

```
Get-Command -Name *variable -Module Microsoft.PowerShell.Utility
```

#### Create Read-only Variables

The `New-Variable` command offers some functionality that isn't available using the variable assignment operator `=`. For example, you can specify that a variable should be read-only, using the `-Option` parameter.

```
New-Variable -Name MyInteger -Value 5
```