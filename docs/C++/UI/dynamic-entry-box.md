# Dynamic Entry Box

Useful to dynamically add button

```cpp title="AnyWidget.h"

UCLASS(Abstract, BlueprintType, meta = (DisableNativeTick))
class SANDBOX_API AnyWidget : public UActivatableBaseWidget
{
	GENERATED_BODY()

private:
	UPROPERTY(meta = (BindWidget, AllowPrivateAccess = true))
	TObjectPtr<UDynamicEntryBox> DynamicEntryBoxButtons;
};
```

## Reset previous buttons

```cpp title="AnyWidget.cpp"
void AnyWidget::ResetPreviousButtons()
{
	if (DynamicEntryBoxButtons->GetNumEntries() != 0)
	{
		DynamicEntryBoxButtons->Reset<UMenuButtonBase>(
			[](const UMenuButtonBase& ExistingButton)
			{
				ExistingButton.OnClicked().Clear();
			}
		);
	}
}
```

## Add new button

```cpp title="AnyWidget.cpp"
void AnyWidget::AddNewButtons()
{
    InputActionRowHandle = ICommonInputModule::GetSettings().GetDefaultBackAction();
	UMenuButtonBase* AddedButton = DynamicEntryBoxButtons->CreateEntry<UMenuButtonBase>();
	AddedButton->SetButtonText(FText::FromString("Anything"));
	AddedButton->SetTriggeringInputAction(InputActionRowHandle);
	AddedButton->OnClicked().AddLambda(
		[this]()
		{
			// Do something on click

			DeactivateWidget();
		}
	);
}
```

## Set focus on specific button (here last)

```cpp title="AnyWidget.cpp"
void AnyWidget::SetFocusOnLastButton()
{
	if (DynamicEntryBoxButtons->GetNumEntries() != 0)
	{
		// Set focus on last button
		DynamicEntryBoxButtons->GetAllEntries().Last()->SetFocus();
	}
}
```