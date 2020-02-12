PowerShell provides an array of built-in commands to manage the filesystem. You can create, retrieve, and delete files and directories.

### Listing Files and Folders

The `Get-ChildItem` command, or `gci` for short, allows you to list files and directories.

```
Get-ChildItem
```

If you want to only retrieve directories, specify the `-Directory` parameter. Conversely, if you want to retrieve only files, use the `-File` parameter.

```
PS > Get-ChildItem -Directory

PS > Get-ChildItem -File
```