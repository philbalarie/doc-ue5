# AnimMontage

## Animation montage

## Convert Manny Anim Montage in C++ 

```cpp title="CustomAnimInstance.h"
#pragma once

#include "CoreMinimal.h"
#include "Animation/AnimInstance.h"
#include "CustomAnimInstance.generated.h"

class UCharacterMovementComponent;
class ACustomCharacter;

UCLASS()
class Custom_API UCustomAnimInstance : public UAnimInstance
{
	GENERATED_BODY()

protected:
	virtual void NativeInitializeAnimation() override;
	virtual void NativeUpdateAnimation(float DeltaTime) override;

private:
	UPROPERTY(BlueprintReadOnly, Category = Reference, meta = (AllowPrivateAccess = "true"))
	TObjectPtr<ACustomCharacter> Character;

	UPROPERTY(BlueprintReadOnly, Category = Reference, meta = (AllowPrivateAccess = "true"))
	TObjectPtr<UCharacterMovementComponent> MovementComponent;

	UPROPERTY(BlueprintReadOnly, Category = Movement, meta = (AllowPrivateAccess = "true"))
	FVector Velocity;

	UPROPERTY(BlueprintReadOnly, Category = Movement, meta = (AllowPrivateAccess = "true"))
	float GroundSpeed;

	UPROPERTY(BlueprintReadOnly, Category = Movement, meta = (AllowPrivateAccess = "true"))
	bool bShouldMove;

	UPROPERTY(BlueprintReadOnly, Category = Movement, meta = (AllowPrivateAccess = "true"))
	bool bIsFalling;
};

```

```cpp title="CustomAnimInstance.cpp"
#include "Character/CustomAnimInstance.h"

#include "GameFramework/CharacterMovementComponent.h"
#include "Custom/CustomCharacter.h"

void UCustomAnimInstance::NativeInitializeAnimation()
{
	Super::NativeInitializeAnimation();

	Character = Cast<ACustomCharacter>(TryGetPawnOwner());
	if (Character)
	{
		MovementComponent = Character->GetCharacterMovement();
	}
}

void UCustomAnimInstance::NativeUpdateAnimation(float DeltaTime)
{
	Super::NativeUpdateAnimation(DeltaTime);

	if (Character == nullptr)
	{
		Character = Cast<ACustomCharacter>(TryGetPawnOwner());
	}
	if (Character == nullptr) return;

	Velocity = MovementComponent->Velocity;
	Velocity.Z = 0.f;

	GroundSpeed = Velocity.Size2D();
	bShouldMove = !MovementComponent->GetCurrentAcceleration().Equals(FVector::ZeroVector, 0.0) && GroundSpeed > 3.f;
	bIsFalling = Character->GetCharacterMovement()->IsFalling();
}
```