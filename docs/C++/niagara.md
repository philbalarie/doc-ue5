# Niagara

## Spawn with onComponentHit

```cpp title="Actor.h"

virtual void BeginPlay() override;

UFUNCTION()
virtual void HandleOnBlasterBeamHit(UPrimitiveComponent* PrimitiveComponent, AActor* OtherActor,
	                                    UPrimitiveComponent* PrimitiveComponent1, FVector NormalImpulse,
	                                    const FHitResult& HitResult);

UPROPERTY(EditAnywhere)
UStaticMeshComponent* BeamMesh;                                        

UPROPERTY(EditAnywhere)
UNiagaraSystem* BlasterBeamEffect;
```

```cpp title="Actor.cpp"

void ABlasterBeam::BeginPlay()
{
	Super::BeginPlay();

	BeamMesh->OnComponentHit.AddDynamic(this, &ABlasterBeam::HandleOnBlasterBeamHit);
}

void ABlasterBeam::HandleOnBlasterBeamHit(UPrimitiveComponent* PrimitiveComponent, AActor* OtherActor,
                                          UPrimitiveComponent* PrimitiveComponent1, FVector NormalImpulse,
                                          const FHitResult& HitResult)
{
	// Spawn VFX effect
	UNiagaraFunctionLibrary::SpawnSystemAttached(BlasterBeamEffect, HitResult.GetComponent(), FName(),
	                                             HitResult.ImpactPoint,
	                                             HitResult.Normal.Rotation(),
	                                             EAttachLocation::Type::KeepWorldPosition, true);
	
}
```