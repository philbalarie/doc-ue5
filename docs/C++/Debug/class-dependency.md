# Class Dependency

When you have class dependencies in blueprint, you can use this to validate the presence of the class on compile in the editor

```cpp title="AnyWidget.h"
UCLASS()
class ANY_API AnyWidget : public UCommonTabListWidgetBase
{
	GENERATED_BODY()
	
private:
#if WITH_EDITOR	
	virtual void ValidateCompiledDefaults(IWidgetCompilerLog& CompileLog) const override;
#endif

UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Frontend Tab List Settings", meta = (AllowPrivateAccess = "true"))
TSubclassOf<UMainMenuCommonButtonBase> TabButtonEntryWidgetClass;

};
```

```cpp title="AnyWidget.cpp"
#if WITH_EDITOR	
void AnyWidget::ValidateCompiledDefaults(IWidgetCompilerLog& CompileLog) const
{
	Super::ValidateCompiledDefaults(CompileLog);
	
	if (!TabButtonEntryWidgetClass)
	{
		CompileLog.Error(FText::FromString(
			TEXT("The variable TabButtonEntryWidgetClass has no valid entry specified. ") +
			GetClass()->GetName() + 
			TEXT(" needs a valid entry widget class to function properly")
		));
	}
}
#endif
};
```