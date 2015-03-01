# Better Network support for Love2d

# Introduction

I'm really surprised to discover always new amazing game.
But I'm also so sad to see most of them are without multiplayer mode.

# Network is hard

Of course I understand why : Lot of people are afraid by network consideration. They are right!

See: [network protocols](url=http://sebsauvage.net/comprendre/tcpip/protocols.pdf).

I dreams to provide an easiest way to share game's data than all game's author should transform their game from solo to multi players.

## Why network is so hard ?

You need to consider :
 * Bandwidth
 * Latency
 * Case of failure (how to return to a usual state)
 * Security (who are allow to read or write what)
 * Attack surface (you should be attack by virus/spammers/... and more from Internet even if you service is for a game)
 * ...

# Current solution

I found : 
 * Love include socket (udp/tcp) and enet.
 * barbes make the [LUBE](https://love2d.org/wiki/LUBE) library that helps to use socket or enet.
 * nothing more?

I think LUBE is a good base for make their own "LAN protocol". But both are low level protocol.

It should be enough to share data over LAN network, because 
 * a big bandwidth (usualy 100M/1000M bps, even 10M bps is often enough) with small latency
 * you trust all connected computers, because all are your friends, there are no security consideration.
 * you will probably don't meet packet lost or disconnection.
 * Most of attacks from Internet are stopped by your router (even you don't know that).

Lot of Game's Author, are bored to think about protocol.

## 1st step

My first step :
 * The client will be run with LÖVE or standalone Lua.
 * The server will be run with nginx+Lua. See [Openresty](http://openresty.org/).
 * Data will be shared over a RESTfull API with the [Lusty a Web Framework](https://github.com/Olivine-Labs/lusty).

### why using a web server ?

The critical point for the server part is :
 * manage lot of connexions
 * manage data (with database)
 * no need graphical/audio stuff (no need SDL/...)
I think web server have exactly the same needs.

## My own game for test

I started with my space game, that is a turn-based game.


# Different kind of need

 * 1. (small-lan) Play with some friends at home (without Internet required) : broadcast, no security (game without password), no closed game needed.

 * 2. (hude-lan) Play with people on LAN-Party : almost like 1 but you need limited game (open/close/kick/ban feature), with or without broadcast, with or without password.

 * 3. (private-net) Play only with friends but over Internet : broadcast are not supported, password or authentication is higtly recommended, transmission probably need encryption (TLS).

 * 4. (public-net) Play with any one over Internet : same than 3 but worst, you need also feature to kick/ban unwanted client (due to insult, flood, ...)



# What the other do ?

## Steam, Origin, Blizzard, ...

You need Internet almost all the time.
Case 1 and 2 without Internet seems denied.
Case 3 and 4 seems ok.


