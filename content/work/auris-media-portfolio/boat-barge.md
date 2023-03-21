---
title: Audio Implementation of a Moving Barge
description: This implementation was done in Unreal Engine 5 and Wwise.
archivesSlug: archives
ShowToc: true
---

I was tasked with implementing audio for a barge, which consisted of a moving wheel. The audio should change in accordance with the speed of the barge, so I have written an audio component blueprint, which would update the BoatSpeed RTPC on Wwise side.

### Unreal Engine

<iframe src="https://blueprintue.com/render/wi48fm6j/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

This function is called every tick from the parent boat blueprint:

<iframe src="https://blueprintue.com/render/nucm7kev/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

Finally everything is tied together by posting the associated Ak event, which plays the barge audio:

<iframe src="https://blueprintue.com/render/8z9v-o2w/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

### Wwise

Inside of Wwise I have created a Boat_Transition Blend Container, which blends the Idle and Moving boat sounds using the BoatSpeed RTPC. Furthermore, Boat_Movement is divided into MotorSounds and WaterSounds, which are further controlled by the BoatSpeed RTPC to change the pitch and volume of these voices.

{{< figure align=center src="barge-wwise.png" >}}

### Results

{{< video src="../BargeSounds.mp4">}}