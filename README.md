
# MLAPI.Relay

## Introduction
The documentation and the relay itself is currently WIP. This is subject to change.

## Configuration
The relay has a config file called config.json. The config contains 3 parts

1. connectionConfig

This is the NetworkTransport connectionConfig. These options have to match up with your games connectionConfig.

2. globalConfig

This is the NetworkTransport GlobalConfig. This instructs the NetworkTransport how the NetworkTransport should work.

3. relayConfig

Relay config contains many different fields.

* maxConnections is the maximum amount of connections the relay can support. 
**THIS HAS TO BE THE SAME ON THE GAME INSTANCE. SEE NOTES**
* port is the relay port
* bufferSize is the size of the buffer that will be allocated for messages
* licenceKey is the licence key you got when purchasing your licence. If this is empty or invalid, a trial licence will be used
* channels is the list of channelTypes that should be used. In the order they are added
* bandwidthGracePeriodLength is the length of the bandwidth grace peridod from the point where a client connects
* gracePeriodBandwidthLimit is the amount of bytes per second that is allowed during the bandwidth grace period for each client. If this 0 or less. No limit will be used during the grace period.
* bandwidthLimit is the amount of bytes per second that is allowed to be used for each client outside of the grace period. If this is 0 or less, no limit will be used.

## Important notes
#### MaxConnections
The relay uses the UNET Transport under the hood. 
The MaxConnections setting is a part of the CRC check that happens during the initial handshake.
By the default the Relay will be setup to handle 4 for the HLAPI config, 100 for the MALPI config and 65534 for Empty. 
This means that if for example you want more than 4 players on the relay and you are using the HLAPI config. 
You HAVE to set the MaxConnections to a larger value on the game instance AND the relay. 
They need to match up.
## Trial licence
The trial licence has no limitations except that only 20 concurrent connections are allowed. 
