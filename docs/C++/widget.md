# Widget

## Creating widget

### Widget

```cpp title="Widget.h"
protected:
	UPROPERTY(EditAnywhere, meta=(BindWidget))
	TObjectPtr<UTextBlock> ObjectiveContent;

	UPROPERTY(EditAnywhere, meta=(BindWidget))
	TObjectPtr<UOverlay> ObjectiveOverlay;

        // Use to bind  widget animation
	UPROPERTY(Transient, meta=(BindWidgetAnim))
	TObjectPtr<UWidgetAnimation> ObjectiveFade;
```   

### Actor

```cpp title="Actor.h"
protected:
	UPROPERTY(VisibleAnywhere, Category = "UI")
	TObjectPtr<UObjectiveWidget> ObjectiveWidget;

	UPROPERTY(EditAnywhere, Category = "UI")
	TSubclassOf<UObjectiveWidget> ObjectiveWidgetClass;
```    

```cpp title="Actor.cpp"
if (ObjectiveWidgetClass)
	{
		ObjectiveWidget = CreateWidget<UObjectiveWidget>(GetWorld()->GetFirstPlayerController(), ObjectiveWidgetClass);
        ObjectiveWidget->AddToViewport();
        ObjectiveWidget->SetVisibility(false);
	    ObjectiveWidget->SetWidgetSpace(EWidgetSpace::Screen);
        // Play an animation in a widget
		ObjectiveWidget->PlayAnimation(ObjectiveWidget->ObjectiveFade, 0.0, 1, EUMGSequencePlayMode::Type::Forward, 1);
	}
	else
	{
		UE_LOG(LogTemp, Error, TEXT("'%s' Miss Objective Widget Class"), *GetNameSafe(this));
	}
```    