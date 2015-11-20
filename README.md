# Better Network support for Love2d

# Introduction

I'm really surprised to discover always new amazing game.
But I'm also so sad to see most of them are without multiplayer mode.

# Network is hard

Of course I understand why : Lot of people are afraid by network consideration. They are right!

See: [network protocols](http://sebsauvage.net/comprendre/tcpip/protocols.pdf).

I dream to provide an easier way to share game's data that all game's author should transform their game from solo to multi players.

## Why network is so hard ?

You need to consider :
 * Bandwidth
 * Latency
 * Case of failure (how to return to a usual state)
 * Security (who are allowed to read or write what)
 * Attack surface (you will be attacked by virus/spammers/... and more from Internet even if you service is for a game)
 * ...

# Current solution

I found : 
 * Love include socket (udp/tcp) and enet.
 * barbes make the [LUBE](https://love2d.org/wiki/LUBE) library that helps to use socket or enet.
 * nothing more?

I think LUBE is a good base to make your custom LAN protocol. But both are low level protocol, not so easy to use.

It should be enough to share data over LAN network, because 
 * a big bandwidth (usualy 100M/1000M bps, even 10M bps is often enough) with small latency
 * you trust all connected computers, because all are your friends, there are no security consideration.
 * you will probably don't meet packet lost or disconnection.
 * Most of attacks from Internet are stopped by your router (even you don't know that).

Lot of Game's Author, are bored to think about protocol.

## 1st step

My first step :
 * The client will run with LÖVE or standalone Lua. See [Technical details](https://github.com/tst2005/love-network/blob/master/client.md).
 * The server will run with nginx+Lua. See [Openresty](http://openresty.org/). See [Technical details](https://github.com/tst2005/love-network/blob/master/server.md).
 * Data will be shared over a RESTfull API with the [Lusty a Web Framework](https://github.com/Olivine-Labs/lusty).

### why using a web server ?

The critical point for the server part is :
 * manage lot of connexions
 * manage data (with database)
 * no need graphical/audio stuff (no need SDL/...)
I think web server have exactly the same needs.

## My own game for test

I started with my space game, that is a turn-based game.


# Different kind of network

 1. (Small-LAN) Play with some friends at home (without Internet required) : broadcast, no security (game without password), no closed game needed.

 2. (Huge-LAN) Play with people on LAN-Party : almost like 1 but you need limited game (open/close/kick/ban features), with or without broadcast, with or without password.

 3. (Private-Net) Play only with friends but over Internet : broadcast are not supported, password or authentication is higtly recommended, transmission probably need encryption (TLS).

 4. (Public-Net) Play with any one over Internet : same than 3 but worst, you need also feature to kick/ban unwanted client (due to insult, flood, ...)


# Different kind of data managment

 A. (FPS-like)

If the game needs very fast refresh of data then you need a permenent connexion between the client and the server.
Working on cached data on the client is not mandatory. The client are able to directly push the action to the server.

 B. (Turn-like)

If your game is slow, It should be good to cache/save data on the client side to be able to restore/resync data between client and server after a disconnection.




# What the other do ?

## Steam, Origin, Blizzard, ...

You need Internet almost all the time.
Case 1 and 2 without Internet seems denied.
Case 3 and 4 seems ok.

## Technical details

* from Valves/Steam : About network : https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking
* from Valves/Steam: About server/client implementation : https://developer.valvesoftware.com/wiki/Networking_Entities
* http://www.gabrielgambetta.com/fast_paced_multiplayer.html
* https://developer.valvesoftware.com/wiki/Latency_Compensating_Methods_in_Client/Server_In-game_Protocol_Design_and_Optimization\
* https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking
* from Unity : http://docs.unity3d.com/Manual/UNetUsingHLAPI.html ; https://bitbucket.org/Unity-Technologies/networking ; http://blogs.unity3d.com/2015/11/19/high-level-multiplayer-networking-layer-has-been-open-sourced/

