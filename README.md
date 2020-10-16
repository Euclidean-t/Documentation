# Euclidean't

<p align="center">
<img width="1340" height="625" src="./Images/Dimensions.png"/>
Team 6<br/>
Aran, Gijs, Inger<br/>
2020-10-16<br/>
</p>

---

## Links
- [Project source](https://github.com/Euclidean-t/Euclidea-N-T)
- [Gameplay video](./Videos/Gameplay.mp4)

## Goal of the project
### Problem
If you want to explore an environment in virtual reality that is bigger than your physical play area, you need a way to move your character through the virtual space. The conventional way of doing this is by moving you virtual character without physically moving, without training this will most likely induce motion sickness.

### Solution
One way to solve this issue is by convining the virtual space within the physical space using non-euclidean geometry. This way the player does not have to move his virtual character and can seamlessly move through the virtual space only using physical movement.

## Technologies
### Virtual reality
Virtual reality is a way to immerse yourself within a virtual environment with limitless potential. It still has some issues, but we want to try and solve one of the issues as described in the goal of the project. 

### Hand tracking
An additional feature now almost always included with virtual reality is hand tracking. When we came up with the idea to use non-euclidean space it seemed interesting to use hand tracking in a way that would desync your hand from the physical space and navigate it separately through the virtual space.


## Design
### Inspiration
The initial idea to use non-euclidean space to navigate a bigger virtual space within your physical play area sparked from Code Parade's ["Non-Euclidean Worlds Engine"](https://youtu.be/kEB11PQ9Eo8?t=245) video on YouTube. We all saw the value in the solution he proposed and it seemed like it had great potential for a VR game.

### Background research
A [blog](https://blog.wetzold.com/) by Wetzold Sutdios was a great help when researching similar virtual reality or non-euclidean games for inspiration. These games include but are not limited to:
- [Tea for God](https://void-room.itch.io/tea-for-god)
- [Spellbound Spire](https://void-room.itch.io/tea-for-god)
- [Sömmad](https://store.steampowered.com/app/676470/Sommad/)
- [Antichamber](https://store.steampowered.com/app/219890/Antichamber/)
- [Shadow Point](https://www.oculus.com/experiences/quest/2088119334554800/?locale=en_US)

### Design process
//TODO: Write about the game idea design and puzzle design

## Created game
//TODO: Write about the gameplay and provide screenshots 

## Difficulties
### Design
//TODO: Write about difficulties creating puzzles in non-euclidean space

### Technology
#### Portals
Creating portals in games is not really that diffucult, it's just a camera projection on a plane. However, it gets quite difficult to do in VR as it requires 2 projections to the same plane in 1 render cycle (1 for each eye). Luckily we found [PocketPortalVR](https://assetstore.unity.com/packages/tools/particles-effects/pocket-portal-vr-85657), a portal solution for VR that uses dimensions relative to the other dimensions, exactly something we could use for our design. It did not work straight out of the box as Valve updated their OpenVR and SteamVR libraries to the Unity OpenXR package, after some work this was resolved. Though to render the portal on both eyes we had to enable multipass rendering which introduced an error on each render cycle, but did not jeopardice the performance as we could see.

As we wanted to track the hands in a way that would separate them from the player when entered another dimension we needed to track if the hand has gone through the portal. This introduced a load of problems as the portal did not use oblique rendering it projected the hand through the portal when it was in front of you, in the other dimension but not on the other side of the portal. We created a way to use oblique rendering when the player was at a distance from the portal, because if we enabled it at all times it would create other problems when morphing the portal plane for player and object transitions.
