# The Hub

A VR space to help people being themselves without the limitations of the "real" Universe.

First of all, the servers should be decentralized. Anyone should be able to host their own world with their own rules.

Otherwise, there should be clients from a VR headset with full body tracking to a basic smartphone so the widest range of people could interact with each other.

## Implementation plan

Remember that this movement is utilitarian? We do the minimum amount of work to achieve maximum profit. So we have to combine the stuff that is already there for maximum profit.

So we start with [Garry's Mod](https://en.wikipedia.org/wiki/Garry%27s_Mod). It's already a great sandbox with extremely full [Steam Workshop](https://steamcommunity.com/app/4000/workshop/).

So first step would be to carefully build an infrastructure to maximize profit from Steam while creating our own infrastructure. We need a need set of programs to download clean game files and Workshop addons locally because they don't work in Steam offline mode.

Once all of that is done, we need to write a [WebAssembly](https://en.wikipedia.org/wiki/WebAssembly) virtual machine in [Lua](https://en.wikipedia.org/wiki/Lua_(programming_language)). Yes, Garry's Mod is crippled by Lua so we'll have to make it run WebAssembly so we can write mods in proper compiled languages such as SScript.

Once all of that is done, we can just move all the code to be a standalone mod on top of [Source SDK 2013](https://developer.valvesoftware.com/wiki/Source_SDK_2013). Here we would have a huge freedom to mod a lot. But we're still stuck with proprietary engine.

So here we finally free ourselves fully by porting the game to [Dæmon engine](https://wiki.unvanquished.net/wiki/Engine). This way we finally have the **full control** over the source code. From there only the sky is the limit.
