# Niagara

Add Niagara dependency

```cs title="File.Build.cs"
PrivateDependencyModuleNames.AddRange(new string[] { "Niagara" });
```

## Spawn with onComponentHit

```cpp title="Actor.h"
class UNiagaraSystem;                              

UPROPERTY(EditAnywhere)
TObjectPtr<UNiagaraSystem> BlasterBeamEffect;

UPROPERTY(EditAnywhere)
TObjectPtr<USceneComponent> BlasterBeamPoint;
```

```cpp title="Actor.cpp"
#include "NiagaraFunctionLibrary.h"

void ABlasterBeam::HandleOnBlasterBeamHit(UPrimitiveComponent* PrimitiveComponent, AActor* OtherActor,
                                          UPrimitiveComponent* PrimitiveComponent1, FVector NormalImpulse,
                                          const FHitResult& HitResult)
{
	// Spawn VFX effect
	UNiagaraFunctionLibrary::SpawnSystemAttached(BlasterBeamEffect, HitResult.GetComponent(), FName("SocketName"),
	                                             HitResult.ImpactPoint,
	                                             HitResult.Normal.Rotation(),
	                                             EAttachLocation::Type::KeepWorldPosition, true);
	
}
```

## Spawn at location

```cpp title="Actor.cpp"
UNiagaraFunctionLibrary::SpawnSystemAtLocation(GetWorld(), BlasterBeamEffect, BlasterBeamPoint->GetRelativeLocation(), BlasterBeamPoint->GetRelativeRotation());
```
