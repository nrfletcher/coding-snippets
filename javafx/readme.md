# JavaFX 

## Why JavaFX?
Firstly, Java is a rich and popular general purpose programming language which means that support will expectedly be long lasting.
Additionally, JavaFX runs on MacOS, Windows, Linux, iOS, Android, and Raspberry Pi. It is heavily cross platform usable.

## Features
JavFX is fully fledged and offers many different components (or widgets like PyQt/Tkinter) to use in your GUI without custom making them.
2D, 3D graphics, charts, WebView, etc.

## Sections
* Core
* Layout
* Basic Controls
* Container Controls
* Web
* Charts
* Additional (fonts, colors, effects, video, audio, etc.)

## Overview
A JavaFX application is based off of a stage which has scenes, and said scenes have scene graphs.
* The stage is an outer frame of our entire application, otherwise thought of as the window (though we can have multiple windows, i.e. multiple stages)
* A scene is what is shown on the stage, and we can at anytime during runtime switch out what scene is being shown (one scene at a time always)
* The scene graph is where all visual components are stored and this is attached to our scene
* All components can be thought of as nodes (they all inherit from javafx.scene.node), some are leafs and some our branches

