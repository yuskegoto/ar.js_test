Web based AR Test with AR.js
by Yuske Goto / at apd
@ yg@yuskegoto.de

Source:
AR.js
https://github.com/jeromeetienne/AR.js/blob/master/README.md


Issues:
-Device restriction
The plugin will currently work only on Android + Chrome Browser, due to the camera device access. However it will be implemented on iOS 11, which will be relesed on Sep.2017.
The pluging also requires secure http connection. Use github repo or your own https server for this.
See also: https://github.com/jeromeetienne/AR.js/issues/45

-Aspectratio
3D models are often squashed or stretched on Android Landscape / Protrait mode.
https://github.com/jeromeetienne/AR.js/issues/60

-iOS workaround
Camera capture is flipped 180 degree, this is due tu a bug on iOS 11 beta.
https://github.com/jeromeetienne/AR.js/issues/90
