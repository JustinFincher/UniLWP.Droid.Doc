Introduction
============

UniLWP.Droid is a live wallpaper (LWP) solution for Unity to run on Android. It is used in most live wallpaper apps from `FinGameWorks <https://play.google.com/store/apps/dev?id=5201975025990666617>`_, including `Metropolis <https://play.google.com/store/apps/details?id=com.justzht.metropolis>`_, `Vortex <https://play.google.com/store/apps/details?id=com.justzht.vortex>`_, and `Diorama <https://play.google.com/store/apps/details?id=com.justzht.lwp.diorama>`_.

UniLWP.Droid is built with customization in mind. It works with Unity's default apk build pipeline, but what makes it different from other solutions is an alternative workflow provided to deeply customize the look and bahavior of your apps through external modifications.


Requirements
------------

- Unity 2019.3 and up (certain features require Unity 2020 or more recent releases)
- Android 7.0 and up (API 24+)
- Android programming experience needed (only if advanced build mode is in use)

Features
--------

- C# callbacks to build data-driven live wallpapers

	- Unlock state (Locked / Ambient / Screen-on / Unlocked)
	- Dark mode
	- Wallpaper scroll offset, with page count and progress on each page
	- Window insets (to avoid overlapped UI rendering with device notch)
	- Is in wallpaper / preview / activity mode

- Unity Ads support 

- Screen saver (DayDream) support

- Non-intrusive integration

	- Unity Cloud Build support

- Customization friendly design

	- Re-building project would still maintain your external modifications made using Android Studio, including java files, xml resources, and gradle dependencies


Version Comparsion
------------------

UniLWP.Droid has two variants. 

- One is `UniLWP.Droid.Free <https://github.com/JustinFincher/UniLWP.Droid.Package.Free>`_, a free plugin in UPM format. 

- Another is `UniLWP.Droid.Store <http://u3d.as/1QVw>`_, an Asset-Store-listed plugin with more features.

+----------------------------+------------+-------------+
| UniLWP.Droid               | Free       |       Store |
+============================+============+=============+
| Unity as Live Wallpaper    | ✅         | ✅          |
+----------------------------+------------+-------------+
| Default Build Pipeline     | ✅         | ✅          |
| (One-Click Apk)            |            |             |
+----------------------------+------------+-------------+
| Callbacks (Lock State,     | ❌         | ✅          |
| Scroll Offset, etc)        |            |             |
+----------------------------+------------+-------------+
| Touch Events               | ❌         | ✅          |
+----------------------------+------------+-------------+
| Modular Customization      | ✅ (You    | ✅ (Editor  |
|                            | need to    | tools       |
|                            | do it      | provided)   |
|                            | yourself)  |             |
+----------------------------+------------+-------------+
| Advanced Build Workflow    | ❌         | ✅          |
+----------------------------+------------+-------------+

Demo
-------------------

