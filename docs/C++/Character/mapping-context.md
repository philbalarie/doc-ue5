# Mapping Context

## Manage multiple mapping contexts

Create actor component and set public function to add mapping context

```cpp title="ExtendedMovementComponent.cpp"
void UExtendedMovementComponent::LinkInputMapping(const APlayerController* PlayerController,
                                                  const EMappingContext InMappingContext)
{
	if (UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(
		PlayerController->GetLocalPlayer()))
	{
		// Subsystem->ClearAllMappings();

		switch (InMappingContext)
		{
		case EMappingContext::MC_Movement:
			Subsystem->AddMappingContext(MovementInputContext, 0);
			break;
		case EMappingContext::MC_UI:
			Subsystem->AddMappingContext(UIInputMappingContext, 0);
			break;
		case EMappingContext::MC_Interaction:
			Subsystem->AddMappingContext(InteractionMappingContext, 0);
			break;
		}
	}
}
}	
```

```cpp title="Character.h"
#pragma once

#include "CoreMinimal.h"
#include "Components/ActorComponent.h"
#include "ExtendedMovementComponent.generated.h"

class UInputMappingContext;

UENUM(BlueprintType)
enum class EMappingContext : uint8
{
	MC_Movement UMETA(DisplayName = "Movement"),
	MC_UI UMETA(DisplayName = "UI"),
	MC_Interaction UMETA(DisplayName = "Interaction")
};

You can create an enum of mapping contexts and set the mapping contexts in Blueprint. It s easier to have all the mapping contexts at the same place.

UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))
class SURVIVALFRAMEWORK_API UExtendedMovementComponent : public UActorComponent
{
	GENERATED_BODY()

public:
	UFUNCTION()
	void LinkInputMapping(const APlayerController* PlayerController, const EMappingContext InMappingContext);

private:
	UPROPERTY(EditAnywhere, meta = (AllowPrivateAccess = true), Category = "01 - MappingContexts")
	TObjectPtr<UInputMappingContext> MovementInputContext;
	
	UPROPERTY(EditAnywhere, meta = (AllowPrivateAccess = true), Category = "01 - MappingContexts")
	TObjectPtr<UInputMappingContext> UIInputMappingContext;
	
	UPROPERTY(EditAnywhere, meta = (AllowPrivateAccess = true), Category = "01 - MappingContexts")
	TObjectPtr<UInputMappingContext> InteractionMappingContext;
};
```