
![](https://i.imgur.com/dJdKQYn.png)

## Introduction
_The documentation and the relay itself is currently WIP. This is subject to change._

The MLAPI.Relay is a relay designed for the UNET Transport to relay traffic between peers that are hidden behind a NAT. Relaying traffic can be expensive but will allow you to communicate no matter what NAT type the host is behind. The MLAPI.Relay works just like the NetworkTransport. Despite the naming, the MLAPI.Relay does not have to be used with the MLAPI library. It can be used with any game built on the NetworkTransport, including the HLAPI. The MLAPI.Relay includes default configurations for use with the MLAPI, HLAPI and an empty template for custom setups. To use the relay simply replace the NetworkTransport with the RelayTransport where the following methods are used:
* Connect
* ConnectEndPoint
* ConnectWithSimulator
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
* Non external licence checking. _Even IF, potentially our servers would go down, or we whould end operation. Your licence will continue to work._

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
* port is the relay port
* bufferSize is the size of the buffer that will be allocated for messages
* updateChecking toggles wheter or not the relay should do web requests to check for updates. This will not by itself enable auto update.
* autoUpdate toggles wheter or not the relay will automatically download and deploy the latest updates. This requires updateChecking to be turned on.
* licenceKey is the licence key you got when purchasing your licence. If this is empty or invalid, a trial licence will be used
* channels is the list of channelTypes that should be used. In the order they are added. Note that some high level libraries have default channels that are added in addition to the user channels. Therefor the relay has templates for the MLAPI default channels and the HLAPI channels. When using these templates, the channels added are only the library channels. User channels have to be added additionaly.
* bandwidthGracePeriodLength is the length of the bandwidth grace peridod from the point where a client connects
* gracePeriodBandwidthLimit is the amount of bytes per second that is allowed during the bandwidth grace period for each client. If this 0 or less. No limit will be used during the grace period.
* bandwidthLimit is the amount of bytes per second that is allowed to be used for each client outside of the grace period. If this is 0 or less, no limit will be used.

## Trial licence
The trial licence has no limitations except that only 20 concurrent connections are allowed. This is to allow for endless evaluation and development.
