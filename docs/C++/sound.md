# Sound

## Play sound at location with attenuation

```cpp title="Actor.h"

UPROPERTY(EditAnywhere, Category = "Blaster Beam")
USoundBase* BlasterSound;

UPROPERTY(EditAnywhere, Category = "Blaster Beam")
USoundAttenuation* BlasterAttenuationSound;
```

```cpp title="Actor.cpp"

// Replace FVector with location
UGameplayStatics::PlaySoundAtLocation(GetWorld(), BlasterSound, FVector(1.f, 1.f, 1.f), 1.f, 1.f, 0.f, BlasterAttenuationSound);
```