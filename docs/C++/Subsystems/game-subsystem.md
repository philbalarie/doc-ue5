# Game Subsystem

Singleton like pattern for unreal

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
	/**
	 * Nice util to get directly subsystem
	 * @param WorldContextObject 
	 * @return 
	 */
	static UFrontendSubsystem* Get(const UObject* WorldContextObject);

	void SetDemoText(FText InDemoText);

	UPROPERTY(EditDefaultsOnly, BlueprintReadWrite)
	FText DemoText = FText::FromString("DemoText");

protected:
	virtual void Initialize(FSubsystemCollectionBase& Collection) override;

	virtual void Deinitialize() override;
};
```

```cpp title="FrontendSubsystem.cpp"
#include "Subsystems/FrontendSubsystem.h"

UFrontendSubsystem* UFrontendSubsystem::Get(const UObject* WorldContextObject)
{
	if (GEngine)
	{
		if (const UWorld* World = GEngine->GetWorldFromContextObject(WorldContextObject, EGetWorldErrorMode::Assert))
		{
			return UGameInstance::GetSubsystem<UFrontendSubsystem>(World->GetGameInstance());
		}
	}

	return nullptr;
}

void UFrontendSubsystem::SetDemoText(FText InDemoText)
{
	DemoText = InDemoText;
}
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