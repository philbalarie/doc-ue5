# Transient

```cpp anyActor.h
	UPROPERTY(Transient)
	TMap<FGameplayTag, UCommonActivatableWidgetContainerBase*> RegisteredWidgetStackMap;
```

A transient variable exists only in memory during runtime and is never written to or read from persistent storage. That's what the comment 'Can not be saved or loaded' actually means.

The nature of it makes it suitable for variables that only need to exist during gameplay or for temporary calculations.

Its value will still persist during runtime unless the owning object gets destroyed and created again. And if that's the case, its value will be reset back to 0.