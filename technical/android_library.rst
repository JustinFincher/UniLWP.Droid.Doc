Android Library
===============

The Android Library here refers to the ``UniLWP-(debug|release).aar`` file located in ``Assets/FinGameWorks/UniLWP/Droid/Plugins`` folder and the source code to compile it. 

The Android Library is responsible for major work of converting an ordinary Unity app into a live wallpaper, including lifecycle modification, manifest declaration, event hijacking, and  C#-Java communications. 

.. Note:: The source code project as a Android Library gradle project, is included as a zip file (``JavaSource.zip``), which you can import using Android Studio to compile your own aar file with own logic.

Contents
--------



Initialization
--------------

UniLWP is designed to initialize even before the Unity player itself for a total control of the player instance. To achieve this goal, it deploys an early-init technique called `ContentProvider <https://developer.android.com/reference/android/content/ContentProvider>`_, which is mainly done in the ``LiveWallpaperInitProvider.java`` file.

.. Tip:: For how Content Provider can be called even before ``Application.onCreate()``, there is a detailed explaination on the `Firebase Dev Blog <https://firebase.googleblog.com/2016/12/how-does-firebase-initialize-on-android.html>`_ as the Firebase SDK also deploys such techniques.

In the ``onCreate()`` method of LiveWallpaperInitProvider, UniLWP calls ``LiveWallpaperManager.Init()`` with the acquired context, which would later be used to create the Unity player.

This way, UniLWP is able to extend its lifespan beyond the Unity player and consequently maintain the control to it no matter the app is launched by system in activity mode or wallpaper mode. The drawback though, is that the Unity player 

Display Target
--------------

Callbacks
---------

Android Module
==============

Contents
--------

Resources
---------