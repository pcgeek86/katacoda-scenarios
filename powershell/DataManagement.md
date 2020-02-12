One of the most powerful capabilities in PowerShell are the native commands it provides to filter, sort, and group objects. Using these commands, it is very easy to harness large data sets containing simple or complex structures.

## Filtering Objects

The following command retrieves a list of all the process objects on the local system, and then pipes (passes) them through a filtration command. The `Where-Object` command discards any objects that don't meet the criteria in the `-FilterScript` ScriptBlock. Inside the `-FilterScript` block, the `$PSItem` automatic variable refers to the "current" item in the pipeline, as PowerShell iterates over each one. We use dot notation to refer to the `Name` property on each `Process` object that is passed from `Get-Process` into `Where-Object`. Aside from the `Name` property, [Process objects](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.process?view=netcore-3.1) have many other useful properties that describe their state.

```
Get-Process | Where-Object -FilterScript { $PSItem.Name -match '^m' }
```

## Sorting Objects

## Grouping Objects