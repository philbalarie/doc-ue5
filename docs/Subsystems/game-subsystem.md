# Game Subsystem

Singleton like pattern for unreal

## Dependency

Need to add "DeveloperSettings" in build file.

## Create Subsystem

```cpp title="FrontendSubsystem.h"
#pragma once

#include "CoreMinimal.h"
#include "Subsystems/GameInstanceSubsystem.h"
#include "FrontendSubsystem.generated.h"

UCLASS()
class SANDBOX_API UFrontendSubsystem : public UGameInstanceSubsystem
{
	GENERATED_BODY()

public:
	UFUNCTION()
	void SetDemoText(FText InDemoText);

	UPROPERTY(EditDefaultsOnly, BlueprintReadWrite)
	FText DemoText = FText::FromString("DemoText");

protected:
	virtual void Initialize(FSubsystemCollectionBase& Collection) override;

	virtual void Deinitialize() override;
};

```
## Access Subsystem

```cpp title="UDemoWidget.cpp"
FText UDemoWidget::GetTextBlockSubsystem()
{
	if (UFrontendSubsystem* FrontendSubsystem = UGameInstance::GetSubsystem<UFrontendSubsystem>(GetWorld()->GetGameInstance()))
	{
		return FrontendSubsystem->DemoText;
	}
	return FText::GetEmpty();
}
```