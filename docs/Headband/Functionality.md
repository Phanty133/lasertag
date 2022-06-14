## Headband team config
1. Make sure headband is off
2. Connect headband to PC via USB
3. Set the team ID via Serial comms
4. Send DONE command to end config
5. Disconnect USB

## Headband-gun linking
1. An unlinked gun is on a reserved RF channel
2. Enter the headband's link mode
	1. Entering the link mode sets the headband's RF channel to the reserved linking channel
3. Shoot headband with the gun to be linked with
4. The headband enters the gun's pipe address which is unique for each gun (Set by gun ID in firmware)
5. The headband and gun exchange linking data over 2.4GHz
	1. Gun receives team ID
	2. Headband receives gun type and stats
6. After the data has been exchanged, the headband send a DONE command to the gun
7. When the headband receives an ACK
	1. The headband and gun enter the active game's RF channel
	2. The headband and gun setup the TX/RX pipes
		1. 1 R/W pair for guns
		2. 1 R/W pair for events (Resupply, grenade, health kit, etc.)

## Link error
1. On link error, flash red, clear config, and reboot

## Status LEDs
- Orange or yellow: Hit
- Flashing orange - Headband battery low
- Blue - In link mode
- Flashing blue - Successful link
- Flashing red - Link error
- Solid red - Player is dead

## Hit registration
1. On hit, process the hit data (Trigger hit with hardware interrupt?)
2. If hit is from an enemy team or friendly fire is on, continue, otherwise break
3. Decrease health
	1. If health <= 0:
		1. Send a DISABLE command to the gun
		2. Send the shooting player a KILL event
		3. Set status to dead
	2. If health > 0:
		1. Send the shooting player a HIT event
		2. Flash status LEDs orange

## On HIT/KILL event receive
- Update local headband statistics