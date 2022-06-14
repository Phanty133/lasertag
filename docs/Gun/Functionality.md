## Status LED
- Green: On
- Flashing orange: Battery Low
- Solid blue: Link mode enabled
- Flashing blue: Link successful
- Flashing red: Link error
- Solid red: Player is dead

## Ammo/Reload
- uC stores an ammo and clip counter
- If out of ammo in clip, press reload button to replenish ammo
	- Reloading takes N seconds
	- Reloading plays a sound effect
- If out of clips and out of ammo in clip, play different sound effect when attempting to fire

## Shooting
The IR beam transmits player/weapon data via digital amplitude modulation

### Data
- Gun ID, 6 bits
- Team ID, 2 bits
- Gun type, 3 bits
- Hamming(15,11) parity, 4 bits

### Transmission
1. Send a series of initial 1ms pulses to synchronize
2. After the init pulses are done, wait for 5?ms on LOW
3. Send data pulses, each 1ms (HIGH for 1, LOW for 0)

## Link error
1. On link error, flash red, reset config to defaults and reboot

## Sound effects
- MicroSD card stores sound effect .wav files
- Speaker to play those dope sound effects