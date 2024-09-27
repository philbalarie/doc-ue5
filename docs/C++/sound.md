# Sound

## Play sound or metasound at location with attenuation

```cpp title="Actor.h"
UPROPERTY(EditAnywhere, Category = "Blaster Beam")
TObjectPtr<USoundBase> BlasterSound;

UPROPERTY(EditAnywhere, Category = "Blaster Beam")
TObjectPtr<USoundAttenuation> BlasterAttenuationSound;
```

```cpp title="Actor.cpp"
// Replace FVector with location
UGameplayStatics::PlaySoundAtLocation(GetWorld(), BlasterSound, FVector(1.f, 1.f, 1.f), 1.f, 1.f, 0.f, BlasterAttenuationSound);
```

## Play sound

```cpp title="Actor.cpp"
#include "Kismet/GameplayStatics.h"

UGameplayStatics::PlaySound2D(GetWorld(), BlasterSound);
```