---
title: Transferring Ultra Dynamic Weather Sounds to Wwise
description: This implementation moves thunder sounds and wind intensity from UDW to Wwise.
archivesSlug: archives
ShowToc: true
---

When dealing with audio in games, it is good to have all audio be located in one Sound Engine. In the game Auris Media was wokring on, the audio for weather was based in Unreal Engine, while Wwise was used for everything else.

After digging around a bit, I have written a small Blueprint Component with functions, which help bridge Wwise and UDW.

This function makes it so that everytime thunder strikes in the game, it sets an RTPC value of LightningDistance and post an audio event at the location of the strike.

<iframe src="https://blueprintue.com/render/be2xlmpl/" scrolling="no" allowfullscreen width="700" height="400"></iframe>

The following small function sets WeatherWind RTPC value, everytime that UDW changes the wind intensity.

<iframe src="https://blueprintue.com/render/u-d8slb-/" scrolling="no" allowfullscreen width="700" height="400"></iframe>