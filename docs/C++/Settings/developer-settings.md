# Component overlap

## Dependency

Need to add "DeveloperSettings" in build file.

## Creating developer setting

```cpp title="DeveloperSettings.h"
#pragma once

#include "CoreMinimal.h"
#include "Engine/DeveloperSettings.h"
#include "FrontendDeveloperSettings.generated.h"

UCLASS(Config = Game, DefaultConfig, meta = (DisplayName = "Frontend Settings"))
class SANDBOX_API UFrontendDeveloperSettings : public UDeveloperSettings
{
	GENERATED_BODY()

public:
	UPROPERTY(Config, EditAnywhere, Category = "Infos Section",
		meta = (ForceInlineRow))
	FName Value;
};
```
## Access developer settings

```cpp title="UDemoWidget.cpp"
FText UDemoWidget::GetTextBlockTest()
{
	const UFrontendDeveloperSettings* FrontendDeveloperSettings = GetDefault<UFrontendDeveloperSettings>();

	if (!FrontendDeveloperSettings->Value.IsEmpty())
	{
		return FrontendDeveloperSettings->Value;
	}

	return FText::FromString("Not defined");
}
```