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

In the ``onCreate()`` method of ``LiveWallpaperInitProvider``, UniLWP calls ``LiveWallpaperManager.getInstance().Init(Context context)`` with the acquired context, which would later be used to create the Unity player.

This way, UniLWP is able to extend its lifespan beyond the Unity player and consequently maintain the control to it no matter the app is launched by system in activity mode or wallpaper mode. The drawback though, is that the Unity player, by default, would be initialized at the beginning, which would let the system took a performance and memory hit early. However, this behavior can be easily tweaked to fit your own need, with the possibility to launch Unity instance when you needed (and destroy it when you don't) through the flag ``unilwp.behavior.isolate`` and those Java APIs:

.. code-block:: java
   :linenos:
   :emphasize-lines: 6,7

    public enum LiveWallpaperManager implements IUnityPlayerLifecycleEvents {
      public static LiveWallpaperManager getInstance() {
         return INSTANCE;
      }

      public void LoadUnity(Context context); // Load Unity instance
      public void UnloadUnity(); // Unload Unity
      public void Init(Context applicationContext); // Load UniLWP, and optionally UniLWP if unilwp.behavior.isolate is false
      public void DeInit(Context applicationContext); // Unload UniLWP and Unity
    }

Display Target
--------------

UniLWP uses a single Unity instance for multiple render targets, including the surface view in activities, wallpaper engine in wallpaper services, and even surface view in screen saver (day dream) services. This shared instance ensures that the contents on those render targets are all the same, the only difference is the rendering resolution. However, UniLWP is required to switch render targets to only the currently active one, or the user would only see a static image.

To make this happen, UniLWP's java plugin calls this method of UnityPlayer when a switch is needed:

.. code-block:: java
   :linenos:
   :emphasize-lines: 4,5

    package com.unity3d.player;
    public class UnityPlayer extends FrameLayout implements IUnityPlayerLifecycleEvents, com.unity3d.player.f {
       public boolean displayChanged(int var1, Surface var2) {
           if (var1 == 0) {
               this.mMainDisplayOverride = var2 != null;
               //...
           }
           return this.updateDisplayInternal(var1, var2);
       }
   }

The method, ``displayChanged(int var1, Surface var2)``, accept two parameters, the first being the display index, while the second is the java `Surface <https://developer.android.com/reference/android/view/Surface>`_ object. Index 0 refers to the main display, as you can see in the highlighted code block. If we supply a value that is bigger than 0, Unity would be updated with the new surface being a `Display <https://docs.unity3d.com/ScriptReference/Display.html>`_ that you can acquire through the C# API `Display[] Display.displays <https://docs.unity3d.com/ScriptReference/Display-displays.html>`_.

However, we are not gonna use this multiple display setup. Instead, UniLWP only uses index 0 for display switches to make existing cameras work without additional efforts. Anytime a new surface is visible, UniLWP calls ``displayChanged(0, newSurface)`` so Unity renders to that surface.

If you are using a customized activity or service, chances are you want your customized surface to be registered into this switch logic. Please refer to :doc:`customize` for more information.

Callbacks
---------

One of UniLWP's unique features is the ability to monitor native events to develop data-driven wallpapers that adapts to dark mode, lock screen, and other device environment changes.

.. Tip:: For how to use callbacks in your C# code, please refer to :doc:`../tutorial/callbacks`

Callbacks are implemented via the ``LiveWallpaperListener`` Java interface and ``LiveWallpaperListenerManager`` Java class.

.. code-block:: java
   :linenos:
   :emphasize-lines: 2,3

   public enum LiveWallpaperListenerManager {
      // called in C#
      protected void setEventListener(LiveWallpaperListener eventListener) {
         this.eventListener = eventListener;
         // report initial status to Unity
         // ...
      }
      private LiveWallpaperListener eventListener;
   }

Behaviour & Flags
-----------------

Android Module
==============

Contents
--------

Resources
---------