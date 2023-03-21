---
title: Implementing Drop Sounds with Velocity
description: This implementation was done in Unreal Engine 5 and Wwise.
archivesSlug: archives
ShowToc: true
---

Drop sounds are great but if the item sounds the same no matter from what height it is dropped, game immersion quickly falls apart.

I was working with already designed item drop sounds and all I needed to do was implement a velocity RTPC, which would change the volume and high-pass filter of the drop voice.

For that, I have written a short function, which based on the vector length at which the dropped item touches the ground and its weight calculates the drop velocity.

<iframe src="https://blueprintue.com/render/t4toim_x/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

This function then calls the Play Drop Sound function, which changes switches in Wwise based on what material the item was dropped on, in turn changing what material sound you hear when the touches the ground and sets the RTPC value for ItemDropVelocity RTPC.

<iframe src="https://blueprintue.com/render/upf05-_r/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

In Wwise the RTPC controls the volume and high-pass filter of the drop sounds using the following graph:

{{< figure align=center src="/images/ItemDropVelocityRTPC.png" >}}