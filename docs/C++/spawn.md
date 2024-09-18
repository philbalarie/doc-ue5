# Spawn

## Spawn actor
```cpp title="actor.cpp"
GetWorld()->SpawnActor<ABlasterBeam>(BlasterBeamClass, Location, Rotation);
```

## Spawn actor with deferred at socket location

```cpp title="actor.cpp"
// Location
const FTransform SocketTransform = BotMesh->GetSocketTransform(SocketName);
ABlasterBeam* BlasterBeam = GetWorld()->SpawnActorDeferred<ABlasterBeam>(BlasterBeamClass, SocketTransform);
// Call that would not be possible with only SpawnActor()
BlasterBeam->SetTargetPawn(TargetPawn);
BlasterBeam->FinishSpawning(SocketTransform);
```