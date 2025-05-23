# Libraries

You can create libraries to act like utils in your projects. Can be used like macros in Blueprint also.

## Debug librarie

```cpp title="DebugLibrary.h"
#pragma once

#include "CoreMinimal.h"
#include "Kismet/BlueprintFunctionLibrary.h"
#include "DebugLibrary.generated.h"

UCLASS()
class SANDBOX_API UDebugLibrary : public UBlueprintFunctionLibrary
{
	GENERATED_BODY()

public:
	UFUNCTION()
	static void DebugPrint(const UObject* WorldObject, const FString& Content, const FLinearColor Color);
};
```

```cpp title="DebugLibrary.cpp"
#include "Libraries/DebugLibrary.h"

#include "Kismet/KismetSystemLibrary.h"

void UDebugLibrary::DebugPrint(const UObject* WorldObject, const FString& Content, const FLinearColor Color)
{
	UKismetSystemLibrary::PrintString(WorldObject, Content, true, true, Color, 2.f, FName("None"));
}

```

