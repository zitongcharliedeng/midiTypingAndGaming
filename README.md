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

- Linnstrument people, for simplicities' sake make sure you turn off pitch and timbre bending otherwise the midi inputs will be less consistent and hard to read.
- The pressure sensor can be left on as it doesn't effect the input IDs, this also means you can bind Linnstrument notes to axis inputs (analog input), you basically have a free Wooting200HE (or 128HE)!!!

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
