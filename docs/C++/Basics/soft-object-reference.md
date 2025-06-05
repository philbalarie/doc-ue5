# Soft object reference

## Create soft pointer

```cpp anyActor.cpp
void AAnyActor::GetSomething(TSoftClassPtr<UWidget> InSoftWidgetClass)
{
	check(!InSoftWidgetClass.IsNull());

	UAssetManager::Get().GetStreamableManager().RequestAsyncLoad(
		InSoftWidgetClass.ToSoftObjectPath(),
		FStreamableDelegate::CreateLambda(
			[InSoftWidgetClass,this]()
			{
				UClass* LoadedWidgetClass = InSoftWidgetClass.Get();

				check(LoadedWidgetClass);

				// Do something with LoadedWidgetClass
			}
		)
	);
}
```