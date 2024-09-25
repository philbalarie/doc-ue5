# Push Widget

Not natively implemented in C++. Need to use a custom method

### Ref

- https://forums.unrealengine.com/t/commonui-how-to-push-a-widget-and-not-have-the-previous-widget-disappear/1521233
- https://smartpoly.teachable.com/courses/ue5-multiplayer-steam-survival-game-course-remastered/lectures/53904961

You need to create an object and use it inside your widget

```cpp title="object.h"

#pragma once

#include "CoreMinimal.h"
#include "UObject/NoExportTypes.h"
#include "CommonActivatableWidget.h"
#include "UIStack.generated.h"

UCLASS(BlueprintType)
class TOWERDEFENSE_API UUIStack : public UObject
{
	GENERATED_BODY()
	
  UPROPERTY()
  TArray<TObjectPtr<UCommonActivatableWidget>> Stack;

  UFUNCTION(BlueprintCallable)
  void PushWidget(UCommonActivatableWidget *Widget);

  UFUNCTION(BlueprintCallable)
  void PopWidget();
};
```

```cpp title="object.cpp"
void UUIStack::PushWidget(UCommonActivatableWidget* Widget)
{
  if (!Stack.IsEmpty())
  {
    Stack[Stack.Num()-1]->DeactivateWidget();
  }
  Stack.Add(Widget);
  Widget->AddToViewport(Stack.Num());
  Widget->ActivateWidget();
}

void UUIStack::PopWidget()
{
  if (!Stack.IsEmpty())
  {
    UCommonActivatableWidget* Widget = Stack[Stack.Num()-1];
    Widget->DeactivateWidget();
    Widget->RemoveFromParent();
    Stack.RemoveAt(Stack.Num()-1);
  }
  if (!Stack.IsEmpty())
  {
    UCommonActivatableWidget* Widget = Stack[Stack.Num() - 1];
    Widget->ActivateWidget();
  }
}
```