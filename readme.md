Web based AR Test with AR.js
by Yuske Goto / at apd
@ yg@yuskegoto.de

Source:
AR.js
https://github.com/jeromeetienne/AR.js/blob/master/README.md

Make own marker
Upload your own marker data (without black sqare) onto Marker Trainer below. It will then return the marker configration file and marker pdf. The picture should be low resolution. I used 240 x 240 pixel. Your design should only be in lower part of the area (lower 1/2 to 1/3).
https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html

How to export 3D Animation from Blender
From blender to JSON is currently only one workflow.
The animation in blender has to have bone, theoretically other deformation should / may also work, but didn't
It's possible to export multiple animations on one data, like walk, idle run etc.
See:
http://unboring.net/workflows/animation.html
https://github.com/arturitu/threejs-animation-workflow
miscellaneous workaround: how to delete unnecessary NLA stack
https://blender.stackexchange.com/questions/36129/can-not-delete-actions-in-action-editor-even-with-shift-x

Issues for ar.js on mobile device:
-Device restriction
The plugin will currently work only on Android + Chrome Browser due to the camera device access. Android Firefox worked partially as well, but camera picture was shown upside down. However it will be implemented on iOS 11, which will be relesed on Sep.2017.
The pluging also requires secure http connection. Use github repo or your own https server for this.
See also: https://github.com/jeromeetienne/AR.js/issues/45

-Aspectratio
3D models are often squashed or stretched on Android Landscape / Protrait mode.
https://github.com/jeromeetienne/AR.js/issues/60

-iOS 11 beta
Camera capture might be flipped 180 degree, this is due tu a bug on iOS 11 beta.
https://github.com/jeromeetienne/AR.js/issues/90

Chrome: Not worked. Probably because of no implementation of WebRTC on Current Chrome version.
Safari: Worked with some issues: See below:
On Portrait Mode: 3D model is vertically stretched
On Horizontal Mode: Vertical Axis (Y) is slanted to right. Model is not stretched.
Above issue is also observed on Android + Chrome (Device: Oppo)
HTC 10 Worked, only on portrait mode and recognized only once.

Hot fix:
For the model stretching issue I implemented a function to switch to models (normal propotion + vertically 50% compressed) according to the device orientation.

Front / Back camera issue
Only on HTC 10 the front camera was activated.
https://github.com/jeromeetienne/AR.js/issues/86