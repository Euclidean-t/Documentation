# Euclidean't

<p align="center">
<img width="640" height="300" src="./Images/Dimensions.png"/><br/>
Team 6<br/>
Aran, Gijs, Inger<br/>
16-10-2020<br/>
</p>

---

## Links
- [Project source](https://github.com/Euclidean-t/Euclidea-N-T)
- [Gameplay video](https://youtu.be/S1Q-OkpVySI)
- Personal reflections
  - [Aran](./Personal/Aran.md)
  - [Gijs](./Personal/Gijs.md)
  - [Inger](./Personal/Inger.md)

## Goal of the project
### Problem
If you want to explore an environment in virtual reality that is bigger than your physical play area, you need a way to move through the virtual space. The conventional way of doing this is by moving your virtual avatar without physically moving. Without training, this will most likely induce dizziness or motion sickness.

### Solution
One way to solve this issue is by confining the virtual space within the physical space using non-euclidean geometry. This way the player does not have to move their virtual avatar separately, and can seamlessly move through the virtual space using only physical movement.

## Technologies
### Virtual reality
Virtual reality is a way to immerse yourself within a virtual environment with nearly limitless potential. It still has some issues, but we want to try and solve one of these issues, as we described in the goal of the project.

### Hand tracking
An additional feature now almost always included with virtual reality is hand tracking. When we came up with the idea to use non-euclidean space it seemed interesting to use hand tracking in a way that would desync your hand from the physical space and navigate it separately through the virtual space.

## Design
### Inspiration
The initial idea to use non-euclidean space to navigate a bigger virtual space within your physical play area sparked from Code Parade's ["Non-Euclidean Worlds Engine"](https://youtu.be/kEB11PQ9Eo8?t=245) video on YouTube. We all saw the value in the solution he proposed, and it seemed like it had great potential for a VR game.

### Background research
A [blog](https://blog.wetzold.com/) by Wetzold Sutdios was a great help when researching similar virtual reality or non-euclidean games for inspiration. These games include but are not limited to:
- [Tea for God](https://void-room.itch.io/tea-for-god)
- [Spellbound Spire](https://void-room.itch.io/tea-for-god)
- [Sömmad](https://store.steampowered.com/app/676470/Sommad/)
- [Antichamber](https://store.steampowered.com/app/219890/Antichamber/)
- [Shadow Point](https://www.oculus.com/experiences/quest/2088119334554800/?locale=en_US)

### Design process
The core concept of our game was quickly found and agreed upon. And, while the portals were added, we started designing the rest of the experience.

We spent the first week ideating, creating features, and the puzzles we could make using them. With the plethora of intriguing directions our initial design could take, we quickly found a challenge in containing the scope of our project to something we could feasibly complete within three weeks.

In the second week, we finalised the design of the puzzles we wanted to create. The creation of puzzles that would work in non-euclidean space also brought its challenges. A life lived in a world ruled strictly by euclidean physics naturally does not train the way of thinking necessary for such a task. The second puzzle, the maze, was by far the most challenging to design. In the final product we had to dial back the scope of this stage. We decided this was necessary partly due to hardware constraints, and partly due to a sudden spike in complexity that was not appropriate for a second stage.

## Created game
We created a non-euclidean puzzle game in VR. In each level, there are one or more buttons that the player has to press before they are given access to the next level. To then get to the next level the player has to walk around the pole, stood in the centre of the room.

### Level 1
In the first level, the player starts in a barren room with nothing but a column in the centre. Walking around the column in the clockwise direction reveals another room. In this room the player finds a button that, when pressed, opens the portal to the next level.

### Level 2
The second level starts in a room with two doorways, each leading to their own dimension. However, one of the doorways is unreachable, as it has a wall in front of it. Going through the open passage reveals the button. But access to this button is still blocked by a wall. In this dimension the other doorway is unblocked. The only way to reach the button would be through the second doorway, but this transports the player to the third dimension of the level, which does not contain a button. The player can only reach the button by walking around the portal before going through again. Doing this brings the player back to the second dimension, now within the walls containing the button. After pressing the button, the player has to return to the third dimension to walk around the pole into the next level.

### Level 3
The third level is more straightforward compared to the second, but it does introduce a new element, a portable portal. Once the player has picked up this portal, they use it to find the button hidden in the other dimension. The player can choose to reach through the portal or go through fully to access this button. Once the button is pressed the way to the next level is opened up in the first dimension.

### Level 4
The fourth level is nearly identical to the third. The only difference being a button can be found in both dimensions. The original idea for this level had the player pressing both buttons at the same time. However, implementing this was of a lower priority than some other features. So in this version, there is no problem when pressing both buttons independently.
This is the last level, walking around the pole one last time will bring you to a room without walls, ceilings or buttons.

## Difficulties
### Design
As touched upon before, designing for non-euclidean space is not the most accessible task. The human mind is generally not accustomed to thinking in more than three dimensions. And the designs made are also not easily translatable to paper. At one point during the creation of the second level, we needed nine diagrams to illustrate the connection between three dimensions that were all connected.

One other problem that did not seem like much of a problem at the start was the countless intriguing approaches we could take. As we went along, we kept stumbling upon ideas for additional features. In this regard, the short deadline probably helped us withhold from overburdening the product with half-finished features.

### Technology
The 2020 version of Unity did not yet support SteamVR natively. Which meant we had to import the Unity asset Valve created. While this asset helped a great deal, it did have a few flaws that we had to work around to get the project functional.

#### Portals
Creating portals in games is not that difficult. It is simply a camera projection on a plane. However, it gets quite difficult to do in VR as it requires two camera projections to the same plane in a single render cycle (one for each eye). Luckily we found [PocketPortalVR](https://assetstore.unity.com/packages/tools/particles-effects/pocket-portal-vr-85657), a portal solution for VR that uses dimensions relative to the other dimensions, which was something we could use for our design. It did not work straight out of the box as Valve updated their OpenVR and SteamVR libraries to the Unity OpenXR package, after some work this was resolved. Though to render the portal on both eyes we had to enable multipass rendering, which introduced an error on each render cycle. Fortunately, this did not jeopardise the performance as far as we could see.

As we wanted to track the hands in a way that would separate them from the player when entered another dimension we needed to track if the hand has gone through the portal. This introduced a load of problems as the portal did not use oblique rendering it projected the hand through the portal when it was in front of you, in the other dimension but not on the other side of the portal. We created a way to use oblique rendering when the player was at a distance from the portal since enabling it at all times would create other problems when morphing the portal plane for player and object transitions.

At the tail end of the development process, we found that there was a bug when placing multiple portals in the same dimension, somehow this introduced recursive rendering when that was should not have been a possibility. We minimalised most of this issue by disabling levels on completion, although sadly this does not remove all the lag. This original goal or reducing motion sickness is not helped by this issue, as lag in VR is similarly motion sickness-inducing.

## PMI
### Plus
- It is quite fun to walk around in such an expansive space when confined to your small physical playing area.
- The result of seamlessly transferring to and from dimensions is satisfying.
- Portals are really fun to work with.
- It is a project that can easily be expanded upon in the future with huge potential.

### Min
- Due to pressure from other courses and the limited development time of 3 weeks it felt a bit like we had to quit in the middle of development.
- Due to corona, the testing process was compromised. We could not physically test it with others, and we had limited access to VR headsets when we were not at home.
- The lag introduced with the bug in the portal software was quite frustrating.
- A lot of the work that had to be done was programming work. After the first week we had most of the design finished.

### Interesting
- Designing levels for non-euclidean space is quite hard because it requires to keep track of the movement of the player in a way that is not natural to us.
- Reducing motion sickness in VR can be both painfully simple and excruciatingly complex.
- We had to change our way of thinking about space to fully utilise the concept of multiple dimensions occupying the same space.


