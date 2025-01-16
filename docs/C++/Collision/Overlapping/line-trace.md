# Line trace

```cpp title="Actor.h"
public:
	UPROPERTY(EditAnywhere, Category = "Line Trace")
	float LineTraceLength = 500.f;
```

```cpp title="Actor.cpp"
void AHorrorBitsCharacter::Interact()
{
	// Center of the screen
	const FVector TraceStart = UGameplayStatics::GetPlayerCameraManager(GetWorld(), 0)->K2_GetActorLocation();
	const FVector TraceEnd = TraceStart + UGameplayStatics::GetPlayerCameraManager(GetWorld(), 0)->GetActorForwardVector() * 50.f;

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