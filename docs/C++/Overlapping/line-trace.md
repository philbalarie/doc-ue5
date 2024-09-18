# Line trace

```cpp title="Actor.h"
public:
	UPROPERTY(EditAnywhere, Category = "Line Trace")
	float LineTraceLength = 500.f;
```

```cpp title="Actor.cpp"
void AHorrorBitsCharacter::Interact()
{
	const FVector TraceStart = FirstPersonCameraComponent->GetComponentLocation();
	const FVector TraceEnd = TraceStart + FirstPersonCameraComponent->GetForwardVector() * LineTraceLength;

    // Debug line
	DrawDebugLine(GetWorld(), TraceStart, TraceEnd, FColor(255, 0, 0), true, 3, 0);

	FHitResult HitResult;
	GetWorld()->LineTraceSingleByChannel(HitResult, TraceStart, TraceEnd, ECC_Visibility);

	if (AActor* Actor = HitResult.GetActor())
	{
		if (Actor->Implements<UInteract>())
		{
			IInteract::Execute_Interact(Actor);
		}
	}
}
```