## Web based AR Test with AR.js
by Yuske Goto / at apd Malaysia
@ yg@yuskegoto.de

This script bases following ar.js mobile performance script from Jerome Etienne.
https://jeromeetienne.github.io/AR.js/three.js/examples/mobile-performance.html

This demo can be tested <a href="https://apd.yuskegoto.de/ar/index.html">here.</a>
Tracking marker is <a href="http://apd.yuskegoto.de/ar/data/ar/apd_tracker.svg">here.</a>

### Source:
AR.js: JavaScript based AR framework, works on AR marker
https://github.com/jeromeetienne/AR.js/blob/master/README.md

Other web-based AR plugins...
Three.js: JavaScript based 3D plugin
https://threejs.org/
a-frame.js: also 3D plugin. three.js wrapper. Simple coding. Slower on mobile devices.

Other web 3D plugins
Blend4web
newly launched, needs evaluation. Seems like promising?
https://www.blend4web.com/en/services/doc/

babylon.js

Make own marker
Upload your own marker data (without black square) onto Marker Trainer below. It will then return the marker configuration file and marker pdf. The picture should be low resolution. I used 240 x 240 pixel. Your design should only be in lower part of the area (lower 1/2 to 1/3).
https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html

How to export 3D Animation from Blender
From blender to JSON is currently only one workflow.
The animation in blender has to have bone, theoretically other deformation should / may also work, but didn't
It's possible to export multiple animations on one data, like walk, idle run etc.
See:
Animation export Blender -> JSON -> three.js
http://unboring.net/workflows/animation.html
https://github.com/arturitu/threejs-animation-workflow
Basic work around with 3D data in Blender -> JSON without animation
https://quaintproject.wordpress.com/2014/01/25/exporting-from-blender-to-web-gl-using-collada-and-three-js-part-2/
https://www.jonathan-petitcolas.com/2015/07/27/importing-blender-modelized-mesh-in-threejs.html
three.js exporter plugin for blender
https://github.com/mrdoob/three.js/tree/master/utils/exporters/blender
miscellaneous workaround: how to delete unnecessary NLA stack
https://blender.stackexchange.com/questions/36129/can-not-delete-actions-in-action-editor-even-with-shift-x

Other 3D formats:
FBX format?
Loading 3DS Max data in three.js with JSON
http://blog.andrewray.me/how-to-export-a-rigged-animated-model-from-3ds-max-three-js/
-three.js accepts also fbx over 7.0 Ascii, but not binary!
-Blender doesn't have 7.0< exporter with Ascii option, so this doesn't work
VRML
3D -> Exportable from blender
Animation -> Blender exporter could not export animation
Gltf
Supposedly the next general web 3D format. But currently there is only web based collada -> gltf converter, which seems like does not export any animation?
https://blog.mozvr.com/a-saturday-night-gltf-workflow/
https://aframe.io/docs/0.6.0/components/gltf-model.html#why-use-gltf

Some issues
ar.js on mobile device:
The plugin will currently work only on Android + Chrome Browser due to the camera device access (WebRTC implementation). Android Firefox worked partially as well, but camera picture was shown upside down. However it will be implemented on iOS 11, which will be relesed on autumn 2017.
The pluging also requires secure http connection. Use github repo or your own https server for this.
See also: https://github.com/jeromeetienne/AR.js/issues/45
Depends on the device's capability for webgl the 3D model on AR screen look different. See device tests below.

-Aspectratio
3D models are often squashed or stretched on Android Landscape / Protrait mode.
https://github.com/jeromeetienne/AR.js/issues/60
Hot fix: For the model stretching issue I implemented a function to switch to models (normal propotion + vertically 50% compressed) according to the device orientation.

Device tests
-iOS 11 beta
Known issue on iOS11 beta: Camera capture might be flipped 180 degree, this is due tu a bug on iOS 11 beta.
https://github.com/jeromeetienne/AR.js/issues/90
Chrome: Not worked. Probably because of no implementation of WebRTC on Current Chrome version.
Safari: Worked with some issues: See below:
On Portrait Mode: 3D model is vertically stretched
On Horizontal Mode: Vertical Axis (Y) is slanted to right. Model is not stretched.

Oppo Android + chrome
Android: 6.0.1
Chrome 59.0.3071.125
Slanted issue is also observed on Android + Chrome (Device: Oppo) -> is this issue due to screen rotation lock?
Slanted issue was solved once screen rotation is turned on.
Animation: little bit jaggy
Directional light: OK
Shadow: Okay

HTC 10
Android Version:
Chrome:
Directional light: OK
Shadow: OK
Animation: OK
It took time to recognize the marker, probably due to loading
Front / Back camera issue
On this device the front camera was activated. Basically ar.js tries to activate "environment" camera = rear camera on initialising.
Related article:
https://github.com/jeromeetienne/AR.js/issues/86

HTC Zenfone 2 Laser (ASUS_Z00ED)
Android Ver 6.0.1
Chrome 59.0.3071.125
Animation was very jaggy
No Shadow

MiPad 2
Android 5.1.0
Chrome 59.0.3071.125
    Animation smooth
    no directional lighting
    no shadow
Firefox test
    Ver: 54.0.1
    Animation: slightly jaggy
    Camera did not focus
    Vertical(Y) axis flipped upside down.
    No directional light
    No shadow
