# midiTypingAndGaming
> "I want to use my Midi input device as a keyboard/ gaming controller on my Windows(?) PC."

This is a guide (for my future self on a new PC) on how to get a Midi Controller working as a fully functional keyboard, with custom layouts if ya like, as well as a video game controller (vJoy) of your liking.
I have only made simple scripts to make the binding process faster, as well as solutions to bugs I encountered on my first time doing it, more like a compilation rather than my own solution!

This is essentially just https://forum.il2sturmovik.com/topic/76764-midi-device-as-game-controller-control-layout-switching-on-the-fly/, but in my own words so my stupid self can understand it quickly in the future.

## Backstory
I absolutely adore my Linnstrument and hate the out of date, skewed qwerty layouts. I've managed to get my Linnstrument to become my main typing keyboard now with this method and having an all in one keyboard (pun intended) feels so nice. The pressure sensors even match the skill ceiling my WootingHE keyboard provides and more!  Not even considered how to use the vertical and horizontal sliding inputs. Now I can just carry my ULTRA keyboard with me where ever I go.

Thus this step by step guide will use a Linnstrument as the Midi input example but any other Midi controller should, potentially, be much easier since they don't have all the confounding settings a Linnstrument can have.

## Requirements
I have only done this on Windows, beware.
May work for other OSs, for Macs, consider forking: https://github.com/gbevin/linnstrument-control
https://www.youtube.com/watch?v=kl--Dp11fPM

# The Guide

## Use midi2vjoy to convert Midi to a vJoy controller.
https://www.youtube.com/watch?v=9ShQVPK3LwM&lc=UgynCBy8Uk4xQ3dXyAV4AaABAg
- Use Spanner's fork which removes the pattern only some Midi controllers follow nowadays https://github.com/spanner-uk/midi2vjoy
- This was his simple change: https://github.com/spanner-uk/midi2vjoy/commit/45452b04f2d732083757868b12916ad5960e9fd2
- He also seems active and responds to common problems in the comments :D Gold mine.
- If it still doesn't work, try search for other forks of midi2vjoy which might suit your use-case better
- Also be open to customizing the python code to debug your controller e.g. if a button is acting like an axis. 

- Linnstrument people, for simplicities' sake make sure you turn off pitch and timbre bending otherwise the midi inputs will be less consistent and hard to read. Also set midi channel to 1 ( i have tried using 16 and for some reason the inputs printed on channel 16 are much harder to decipher, for channel 1 it is always beginning with 160...) MAKE SURE SPLIT IS TURNED OFF, basically make sure the midi inputs are as little tampered and as simple as possible, you can make a preset for this.
- The pressure sensor can be left on as it doesn't effect the input IDs, this also means you can bind Linnstrument notes to axis inputs (analog input), you basically have a free Wooting200HE (or 128HE)!!! make sure to push the keys dead center when testing for input ids
- - These settings ( Linnstrument on +5 default tuning, midi chanenel 1 , disabled split, bend and timbre, one chan midi mode.... no overlap) should yield you midi inputs that follow a pattern and can be predicted, there for we dont need to measure every single input id manually and instead we can use my python script:

My Linnstrument Preset when Using as Typing Keyboard (and recording its inputs):
1.) RESET TO DEFAULT FIRST
2.) PERSPLIT: Channel Per Note (otherwise 2 notes share the same id used in midi2joy, which is bad), Midi CHannel 1, Bend+96(holddown24andslideup), X OFF, Y OFF
3.) Press preset and Save as a preset so you can switch to and fro.
---
> From the Linnstrument manual:
At the right side of the Preset screen are 4 blue-lit note pads indicating 4 "All Settings" memories. Each of these 4 memories holds a snapshot of all Per-Split Settings, Octave/Transpose settings and Global Settings (Note that the Preset and Volume screen settings are not included because the intent is to instantly change all of LinnStrument’s settings but not the preset and volume of external MIDI sound generators).

To save the current LinnStrument settings to one of these 4 memories, hold one of the 4 blue-lit note pads for 2 seconds or more.

To recall the saved settings, briefly tap one of these 4 buttons.
Cheers!


---



- Manually writing up the bindings in the midi2vjoy config file is the slowest part, so I made a python script to do it for me:
- See the repo folder ABC and download, then input... then run... Y
- 
## Use joystickGremlin to convert vJoy controller to keyboard keys OR better joystick binds/ configs (e.g. alter sensitivity of joysticks, activations points... such a good software that gremlin...)
- Ensure that in the Settings tab (NOT THE OPTIONS TAB), next to all your Joy input and vJoy input devices, **you enable your vJoy #X to be used as an input**!!!
- It is off by default since Gremlin uses vJoy as the output from the altered Joy inputs (Joy meaning like regular game controllers, Joystick you get me? vJoy is a virtual Joystick made by vJoy).

- Pro tip, make sure Gremlin isn't activated and go to the vJoy device tab, click the Midi button you want to bind (assuming midi2joy is still running in the background) and although it won't auto scroll in the left window, the binding in the right window will be for the key you just pressed. You can manually do this for each key and assign the new binds or use my script with GUI:
# Future Plans

- Make all this happen from one click (except from a provided config file for my preferred keyboard layout and stuff)
- - So i can plug in my ULTRAkeyboard into any (Windows?) system and within seconds, use it as THE ULTRAkeyboard.
- Make a Mouse Macro to toggle between Midi and KeyboardGaming mode, since you don't have access to the "keyboard" in Midi mode if you are entirely replacing your typing keyboard like me
- -- Or have the macro built into Linnstrument somehow, gbevin did this by detecting when LinnStrument is set to OS Update mode, his app LinnStrument Control detects its presence and takes control over it.
- - Another program to analyse for inspiration is https://github.com/flipcoder/midimech. So cooool
