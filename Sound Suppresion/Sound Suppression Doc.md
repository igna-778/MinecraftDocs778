# Sound Suppression
Sound suppression is a new type of suppression like OOM, ClastCast (shulker suppression) and StackOverflow (pre 1.18 suppression) that uses the tile entity swap technic to create a tile entity in a illegal state which can later be used to suppress.

#### Credit:
- Original Discovery
	- JKM
	- Metacinabar
- Making a More Usable Version
	- Igna778
- Research And Development People
	- Lame
	- Savva
	- Void
	- Ruthro

```ad-help
title: Need Help?
Sound Suppresion Showcase Video: https://youtu.be/77M8Adnxmsw?si=f-hon2OtKevtEUhx

Youtube Chanel:https://youtube.com/@igna778
Discord Comunity: https://discord.gg/rsuTZer7RT
```

## On the Practical side
This exploit has major practical applications as well as a big probability of becoming a crashing hazard if used incorrectly so its should always be treated with caution.

### The setup

#### Building It
The setup consists of a calibrated sculk suppressor an observer with a noteblock and a door next to a carpet block placed on top of the sculk sensor. It is all set up as follows:

```ad-warning 
title: Door State
Its important to point out that in the setup here the door is in an Off state and should be placed exactly like this
```

![[Pasted image 20240806104831.png|350]]

![[Pasted image 20240806105705.png|350]]

The rail line shown, which is a budded rail line should be connected to a update suppressor, if you are in 1.20 and you have a CCE Box you should use that for the setup, Otherwise you can go with the latest OOM setup (As of the writing of this Snowball Suppression).

```ad-info 
title: 1.19 sound suppresion
1.19 sound suppression isnt really stable as there is no way to controll the sound channels as such you should try to get a CCE box and later upgrade it when you are in 1.20
```

### Using it
To use the setup just stand in front of the door wile it opens an closes and try to break te bottom part of the door with a diamond hoe, onces it opens you will instad break the calibrated sculk sensor and trigger the suppression.

After that replace the door with a comparator and place a lectern **with a book containing 15 pages**

![[Pasted image 20240806105705.png|350]]

![[Pasted image 20240806111136.png|350]]

```ad-tip
title: Tip
Whait a few minutes until you are sure the server has finish processing the suppresion. Especialy if you are using OOM.
```

```ad-danger
title: Extreme Caution Next Step
If the next step is preformed incorrectly you could crash loop yourself. BE CAREFULL!!
```

Grab a chest and face the comparator, that way you make sure the chests back is getting powered by the comparator. Place the chest where the calibrated sculk sensor used to be. 

![[Pasted image 20240806111756.png]]

### Breaking it

```ad-danger
title: Extreme Caution Next Step
If the next step is preformed incorrectly you could crash loop yourself. BE CAREFULL!!
```

If you plan on no longer using the setup break the chest before any other component. **Breaking the comparator or Lecter will probably crash loop you**. 

## Sound Channels
The sound suppressor has 15 sound channels but I only found useful the following ones. If you find anything out and think this document should be updated please contact Igna778 through discord.

```ad-warning
title: Non player actions
Remeber non player actions could crash the server, things such as using rockets or creepers blowing up stuff could case the server to go down
```

##### 1 Movement in any medium
- **Kick exploit**
	- Kicks any player that is making a sound while moving
##### 4 Gliding with an elytra or unique mob actions
- **Fly Kick**
	- If you fly with elytra you will get kick
- **Shadow Items**
	- You can create shadow items with armor stands if they have hands
##### 5 Dismounting a mob or equipping gear
- **Shadow Items**
	- You can create shadow items of armor items
##### 7 Mobs and players getting damaged
- **Damage Animation Cancel**
	- Cancels the damage animation
##### 9 Blocks 'deactivating'
- **Can be used to create small suppression**
	- Using noteblocks or trapdoors you can create a normal suppressor
##### 10 Blocks 'activating'
- **Can be used to create small suppression**
	- Using noteblocks or trapdoors you can create a normal suppressor
##### 12 Non-wool blocks being destroyed
- **In destructible blocks**
	- Makes every block in range (except wool and custom breaking blocks like doors) indestructible
##### 13 Place Blocks
- **Dupe**
	- You can dupe any block you place

```ad-note
title: Other chanels
Atleast from what found initaly other chanels just kick / crash the server, some might be usefull in realy specific situations but wont be addreased in this document 
```


## Code digging
```ad-info
title: Code Mappings
All of the code paths, clases methods and else names are taken from the yarn mappings of the game
```

This exploit is posible thanks to the `blockstate` part of the of getting a property which does not exist in the `blockstate`. The relevant classes to this exploit are: `CalibratedSculkSensorBlockEntity`, `State` and `Vibrations`
#### Call Hierarchy
When creating a game event (vibration) the game looks for listeners to relay that information to. In this case the `CalibratedSculkSensorBlockEntity` is one of those listeners and the code that works out if the game event (vibration) should be accepted is executed.

```java
	public boolean listen(ServerWorld world, RegistryEntry<GameEvent> event, GameEvent.Emitter emitter, Vec3d emitterPos) {  
    ListenerData listenerData = this.receiver.getVibrationListenerData();  
    Callback callback = this.receiver.getVibrationCallback();  
    if (listenerData.getVibration() != null) {  
        return false;  
    }  
    if (!callback.canAccept(event, emitter)) {  
        return false;  
    }  
    Optional<Vec3d> optional = callback.getPositionSource().getPos(world);  
    if (optional.isEmpty()) {  
        return false;  
    }  
    Vec3d vec3d = optional.get();  
    if (!callback.accepts(world, BlockPos.ofFloored(emitterPos), event, emitter)) {  
        return false;  
    }  
    if (VibrationListener.isOccluded(world, emitterPos, vec3d)) {  
        return false;  
    }  
    this.listen(world, listenerData, event, emitter, emitterPos, vec3d);  
    return true;}
```

The first call `accepts` is the place were the crash happens.

```java
public boolean accepts(ServerWorld world, BlockPos pos, RegistryEntry<GameEvent> event, @Nullable GameEvent.Emitter emitter) {  
    int i = this.getCalibrationFrequency(world, this.pos, CalibratedSculkSensorBlockEntity.this.getCachedState());  
    if (i != 0 && Vibrations.getFrequency(event) != i) {  
        return false;  
    }  
    return super.accepts(world, pos, event, emitter);  
}
```

If the `blockstate` doesn't have a direction property it will crash in the `getCalibrationFrequency` before doing the check for the vibration channel, otherwise it will check if the vibration corresponds to the frequency set by the Redstone power and if it is it will later crash in the `super.accepts` part of the code. 

## Document Credit
Thanks to everyone who contributed to this document.
#### Creator
- Igna778
#### Contributors
- krispyking24
- infernal
