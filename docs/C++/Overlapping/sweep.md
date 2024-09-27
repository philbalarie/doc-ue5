# Sweep

Doc for sweep: https://unrealcpp.com/sweep-multi-line-trace/

## Single

```cpp title="Actor.cpp"
const ACharacter* PlayerCharacter = UGameplayStatics::GetPlayerCharacter(GetWorld(), 0);
const FVector ActorLocation = PlayerCharacter->GetActorLocation();
const FVector SweepStart = ActorLocation - FVector(0.f, 0.f, 30.f);
const FVector SweepEnd = ActorLocation - FVector(0.f, 0.f, 30.f);
const FCollisionShape ColSphere = FCollisionShape::MakeSphere(SphereRadius);
FHitResult TraceResult;

// Debug Collision
DrawDebugSphere(GetWorld(), ActorLocation, ColSphere.GetSphereRadius(), 50, FColor::Purple,
	                true);

GetWorld()->SweepSingleByChannel(TraceResult, SweepStart, SweepEnd, FQuat::Identity, ECC_Visibility, ColSphere);

if (AActor* OtherActor = TraceResult.GetActor())
	{
		if (OtherActor->Implements<UInteract>())
		{
			if (const AItem* Item = Cast<AItem>(OtherActor))
			{
				// Pass the inventory to the Interact
				Item->Execute_Interact(TraceResult.GetActor(), this);
			}
		}
	}
```

## multi

```cpp title="Actor.cpp"
const FVector ActorLocation = this->GetActorLocation();
const FVector SweepStart = ActorLocation - FVector(0.f, 0.f, 30.f);
// End location need to be slightly different to work https://forums.unrealengine.com/t/why-does-sweepsinglebychannel-not-work-with-a-box/393240/3
const FVector SweepEnd = ActorLocation - FVector(0.f, 0.f, 30.1);
const FCollisionShape ColSphere = FCollisionShape::MakeSphere(120.f);
TArray<FHitResult> TraceResult;

// Debug Collision
DrawDebugSphere(GetWorld(), ActorLocation, ColSphere.GetSphereRadius(), 50, FColor::Purple, true);

GetWorld()->SweepMultiByChannel(TraceResult, SweepStart, SweepEnd, FQuat::Identity, ECC_Visibility, ColSphere);

for (FHitResult Result : TraceResult)
	{
		if (AActor* OtherActor = Result.GetActor())
		{
			if (OtherActor->Implements<UInteract>())
			{
				if (const ADoor* Door = Cast<ADoor>(OtherActor))
				{
					Door->Execute_Interact(Result.GetActor());
					return; // If you want only the first result
				}
			}
		}
	}
```