
![](https://i.imgur.com/dJdKQYn.png)

## Introduction
The documentation and the relay itself is currently WIP. This is subject to change.

The MLAPI.Relay is a relay designed for the UNET Transport to relay traffic between peers that are hidden behind a NAT. Relaying traffic can be expensive but will allow you to communicate no matter what NAT type the host is behind. The MLAPI.Relay works just like the NetworkTransport. To use the relay simply replace the NetworkTransport with the RelayTransport where the following methods are used:
* Connect
* AddHost
* AddHostWithSimulator
* AddWebsocketHost
* Disconnect
* Send
* QueueMessageForSending
* SendQueuedMessages
* Receive
* ReceiveFromHost

## Features
* Written in .NET Core for Cross platform
* Allows you to limit bandwidth (optional)
* Update checking (optional). _This will check for updates and inform you of new updates._
* Deploy and forget Auto-update (optional). _The auto update feature allows you to deploy the relay and it will auto update whenever needed._
* Disable home calling. _The MLAPI will only do connections to external sources for update checking purposes. This can be disabled._

## Matchmaking
Unlike Unity's relay. The MLAPI.Relay does not require you to use any specific matchmaker. The MLAPI.Relay will pass the destination address when connecting rather than a relay specific roomId. This allows you to run the MLAPI.Relay with any matchmaker or without a matchmaker all together.

## Special setup
The MLAPI.Relay REQUIRES there to be at least ONE reliable channel type. If it is plain reliable or has sequencing or fragmenting support does not matter.

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
* updateChecking toggles wheter or not the relay should do web requests to check for updates. This will not by itself enable auto update.
* autoUpdate toggles wheter or not the relay will automatically download and deploy the latest updates. This requires updateChecking to be turned on.
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
