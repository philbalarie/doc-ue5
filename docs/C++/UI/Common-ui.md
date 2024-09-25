# Common UI

## Configuration

Need to add UMG and CommonUI in build file to prevent build fail.

```cpp title=file.Build.cs
PublicDependencyModuleNames.AddRange(new string[] { "UMG", "CommonUI" });
```