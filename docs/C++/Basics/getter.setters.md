# Getters and setters

## Generate getters and setters

```cpp anyObject.h
#pragma once

#include "CoreMinimal.h"
#include "AnyObject.generated.h"

#define LIST_DATA_ACCESSOR(DataType,PropertyName) \
FORCEINLINE DataType Get##PropertyName() const { return PropertyName;} \
void Set##PropertyName(DataType In##PropertyName) { PropertyName = In##PropertyName;}

UCLASS()
class ANYPROJECT_API UAnyObject : public UObject
{
	GENERATED_BODY()

public:
	LIST_DATA_ACCESSOR(FName, DataID)
	LIST_DATA_ACCESSOR(FText, DataDisplayName)
	
private:
	FName DataID;
	FText DataDisplayName;

};
```

Can be used like this in cpp file:

```cpp anyObject.cpp
AnyObject->GetDataID();
AnyObject->SetDataID();
```