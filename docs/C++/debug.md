# Debug

## On screen message

### With parameter

```cpp title="Actor.cpp"
GEngine->AddOnScreenDebugMessage(-1, 15.0f, FColor::Yellow, FString::Printf(TEXT("Player take damage: %f"), Health));
```               

### Without parameter

```cpp title="Actor.cpp"
GEngine->AddOnScreenDebugMessage(-1, 15.0f, FColor::Yellow, TEXT("Test"));
```    
