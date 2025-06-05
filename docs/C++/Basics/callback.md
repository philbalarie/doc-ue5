# Callback

```cpp title="widget.h"
UENUM(BlueprintType)
enum class EActionType : uint8
{
	Confirmed,
	Cancelled,
};

UCLASS()
class SANDBOX_API UDemoWidget : public UUserWidget
{
	GENERATED_BODY()

	void SetCallbackText(FText Value, const TFunction<void(EActionType)>& SetTextCallback);
	

protected:
	virtual void NativeConstruct() override;
	
};
```

## Spawn at location

```cpp title="widget.cpp"
void UDemoWidget::SetCallbackText(FText Value, const TFunction<void(EActionType)> &SetTextCallback)
{
	TextBlockCallback->SetText(Value);
	
    // Call callback
	SetTextCallback(EActionType::Confirmed);
}

void UDemoWidget::NativeConstruct()
{
	SetCallbackText(FText::FromString("Callback Text"),
    // Pass callback
		[this](EActionType ActionType)
		{
			UE_LOG(LogTemp, Warning, TEXT("Calling from callback with ActionType: %hhd"), ActionType)
		});
}
```
