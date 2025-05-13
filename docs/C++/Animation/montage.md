# Montage

## Play montage

```cpp title="Actor.h"
UPROPERTY(EditAnywhere)
TObjectPtr<UAnimMontage> FireAnimation;
```

```cpp title="Actor.cpp"
UAnimInstance* AnimInstance = Character->GetMesh1P()->GetAnimInstance();
AnimInstance->Montage_Play(FireAnimation, 1.f);
```