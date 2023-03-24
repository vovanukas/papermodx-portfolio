---
title: Transferring Ultra Dynamic Weather Sounds to Wwise
description: This implementation moves thunder sounds and wind intensity from UDW to Wwise.
archivesSlug: archives
ShowToc: true
---

When dealing with audio in games, it is good to have all audio located in one Sound Engine. In the game, Auris Media was working on, the audio for the weather was based in Unreal Engine, while Wwise was used for everything else.

After digging around a bit, I have written a small Blueprint Component with functions, which help bridge Wwise and UDW.

This function makes it so that every time thunder strikes in the game, it sets an RTPC value of LightningDistance and posts an audio event at the location of the strike.

<iframe src="https://blueprintue.com/render/be2xlmpl/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

The following small function sets the WeatherWind RTPC value, every time that UDW changes the wind intensity.

<iframe src="https://blueprintue.com/render/u-d8slb-/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

You may notice that these RTPCs don't have an actor component, that is due to the weather being handled client side, thus not requiring an actor input to be GameObject based.