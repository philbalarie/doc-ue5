# Timeline

## Timeline with curve

```cpp title="Actor.h"
public:
	ADoor();

	UPROPERTY(EditAnywhere, Category = "Timeline")
	TObjectPtr<UTimelineComponent> OpenDoorTimeline;

	UPROPERTY(EditAnywhere, Category = "Timeline")
	TObjectPtr<UCurveFloat> OpenDoorCurve;

	UFUNCTION()
	void RotateToOpenDoor(float InterpolatedVal);

protected:
	virtual void BeginPlay() override;    
```

```cpp title="Actor.cpp"
ADoor::ADoor()
{
	OpenDoorTimeline = CreateDefaultSubobject<UTimelineComponent>(TEXT("OpenDoorTimeline"));
}

void ADoor::BeginPlay()
{
	if (OpenDoorTimeline != nullptr && OpenDoorTimeline != nullptr)
	{
		FOnTimelineFloat OnTimelineFloat;
		OnTimelineFloat.BindDynamic(this, &ADoor::RotateToOpenDoor);

		OpenDoorTimeline->AddInterpFloat(OpenDoorCurve, OnTimelineFloat);
	}
	else
	{
		UE_LOG(LogTemp, Error, TEXT("'%s' Miss OpenDoorCurve"), *GetNameSafe(this));
	}
}

// Example with a door rotation
void ADoor::RotateToOpenDoor(float InterpolatedVal)
{
	const float ZRotation = FMath::Lerp(0, -90.f, InterpolatedVal);
	DoorMesh->SetRelativeRotation(FRotator(0, ZRotation, 0));
}
```