# Custom Trace Channel

Need to be set in Project settings / Traces.

You pass ECC_GameTraceChannel with the correct index 1 -18. Those are the custom ones defined in the editor.

```cpp title="Actor.cpp"
void ACookingSimulatorCharacter::Interact(const FInputActionValue& Value)
{
	GetWorld()->SweepSingleByChannel(TraceResult,
		SweepStart,
		SweepEnd,
		ECollisionChannel::ECC_GameTraceChannel1, ColSphere);
}
```