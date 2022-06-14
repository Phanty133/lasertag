## Base config
- For now: set station team ID in code

## Resupply
1. When the buttons is pressed, the base station sends a DISTANCE command to everyone in the event pipe (Command tagged with team ID)
2. When a headband receives a DISTANCE command with its team ID, the headband sends 100 packets with its unique ID
3. The base station counts how many packets get dropped from each ID
4. Send a RESUPPLY command to all headband IDs, that have dropped packets less than N (Signal strength is strong enough, i.e. player is close to the station)
5. When a headband receives a RESUPPLY command
	- Reset health
	- Send RESUPPLY command to the gun