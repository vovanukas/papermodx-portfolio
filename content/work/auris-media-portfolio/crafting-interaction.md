---
title: Implementing Crafting Interaction with Unique Item Sounds
description: This implementation was done in Unreal Engine 5 and Wwise.
archivesSlug: archives
ShowToc: true
---

Crafting systems are an essential part of many video games, allowing players to combine resources and create new items or upgrades.

While working in Auris Media, one of the harder challenges I faced was sound implementation for the underlying crafting system due to the client-server replication environment.

Using custom replicated events, I was able to create triggers for when a player starts, finishes, cancels, fails crafting. But due to how the crafting in the game works, there was no trigger for when a player starts crafting next item in the crafting queue, so I had to get creative for that.

<iframe src="https://blueprintue.com/render/ho69zfp2/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

### Implementation

To address the challenges posed by client-server replication, I utilized custom replicated events to create triggers for different crafting stages. Let's explore the implementation steps:

#### Crafting Start Sound:
When a player starts crafting, the `PlayCraftingStartAudio` event is fired. This event passes the `Item` variable, which contains information about the crafted item. Using a custom function called `GetItemSound`, I extracted the crafting loop sound specific to the item. This sound is then played using the `PostEvent` function in Wwise.

#### Crafting Completion Sound:
Upon completing the crafting process, the `PlayCraftingFinished` event is triggered. First, I accessed the `BlueprintsQueue` using the `GetBlueprintsQueue` function, with the `CraftingComponent` of the player as the target. It's important to note that I modified the `BlueprintsQueue` to be Replicated to ensure consistency between the client and server.

Next, I played the crafting completion sound using the `PostEvent` function. This sound signifies the successful creation of the item. Additionally, in the second `PostEvent` function, I stopped the previously playing crafting loop sound to prevent any overlap.

#### Handling Multiple Blueprints:
To handle cases where multiple items of same blueprint are in the crafting queue, I added a branch in the blueprint. If there are remaining items in the queue, the `PlayCraftingStartAudio` event is fired again. This time, the `Item` variable is obtained using the `GetItemFromBlueprintInBlueprintQueue` macro, which fetches the item from `BlueprintsQueue[0]`.

#### Completing the Crafting Process:
In scenarios where there is only one item remaining in the crafting queue, I added another branch. Here, I checked if there are additional blueprints in the `BlueprintQueue` array. If so, the `PlayCraftingStartAudio` event is triggered again, passing the item from the next blueprint (accessed through `BlueprintQueue[1]`, using the `GetItemFromBlueprintInBlueprintQueue` macro). This allows for a smooth transition to crafting the next item.

If no more blueprints are present in the queue, no action is taken, as the crafting audio loop has already been stopped.

### Results

This implementation allows for the addition of custom crafting loop, crafting start and crafting complete sounds for items based on their properties and enhances the audio experience for the players.

{{< video src="../crafting-loop.mp4">}}