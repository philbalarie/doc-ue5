# Gameplay Tags

Add Gameplay Tags dependency

```cs title="File.Build.cs"
PrivateDependencyModuleNames.AddRange(new string[] { "GameplayTags" });
```

## Create gameplay Tags

```cpp title="FrontendGameplayTags.h"
#pragma once

#include "NativeGameplayTags.h"

namespace FrontendGameplayTags
{
	// Frontend widget stack
	JHONNYCANCOOK_API UE_DECLARE_GAMEPLAY_TAG_EXTERN(Frontend_WidgetStack_Modal)
}
```

## Spawn at location

```cpp title="FrontendGameplayTags.cpp"
namespace FrontendGameplayTags
{
	// Frontend widget stack
	UE_DEFINE_GAMEPLAY_TAG(Frontend_WidgetStack_Modal, "Frontend.WidgetStack.Modal")
}
```

## Access gameplay Tags

```cpp title="AnyActor.cpp"
FrontendGameplayTags::Frontend_WidgetStack_Modal
```

## Force some tags in parameter

```cpp title="anuActor.h"
	UFUNCTION(BlueprintCallable)
	void RegisterWidgetStack(UPARAM(meta = (Categories = "Frontend.WidgetStack")) FGameplayTag InStackTag);
```