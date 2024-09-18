# Timer

## Creating a timer

```cpp title="actor.h"
UFUNCTION()
void SpawnBlasterBeam();

UPROPERTY(EditAnywhere)
float BlasterBeamTimer = 1.f;
```

```cpp title="actor.cpp"
FTimerHandle Timer;
GetWorldTimerManager().SetTimer(Timer, this, &ABot::SpawnBlasterBeam, BlasterBeamTimer, true);
```

If using component instead of actor, need to call GetOwner before.

```cpp title="component.cpp"
FTimerHandle ReverseTimer;
GetOwner()->GetWorld()->GetTimerManager().SetTimer(ReverseTimer, this, &UNotificationComponent::ReverseFadeAnimation, 3, false);
```