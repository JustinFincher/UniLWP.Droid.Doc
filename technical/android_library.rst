Android Plugin
==============

The scope of this page is within ``Assets/FinGameWorks/UniLWP/Droid/Plugins`` and the source files that contributed to the plugins in that folder.

Android Library
---------------

The Android Library here refers to the ``UniLWP-(debug|release).aar`` file located in ``Assets/FinGameWorks/UniLWP/Droid/Plugins`` folder and the source code to compile it. 

The Android Library is responsible for major work of converting an ordinary Unity app into a live wallpaper, including lifecycle modification, manifest declaration, event hijacking, and  C#-Java communications. 

.. Note:: The source code project as a Android Library gradle project, is included as a zip file (``JavaSource.zip``), which you can import using Android Studio to compile your own aar file with own logic.

Initialization
^^^^^^^^^^^^^^

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
^^^^^^^^^^^^^^

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
^^^^^^^^^

One of UniLWP's unique features is the ability to monitor native events to develop data-driven wallpapers that adapts to dark mode, lock screen, and other device environment changes.

.. Tip:: For how to use callbacks in your C# code, please refer to :doc:`../tutorial/callbacks`

Callbacks are implemented via the ``LiveWallpaperListener`` Java interface and ``LiveWallpaperListenerManager`` Java class.

.. code-block:: java
   :linenos:
   :emphasize-lines: 2,3

   public enum LiveWallpaperListenerManager {
      // called in C# via AndroidJavaObject
      protected void setEventListener(LiveWallpaperListener eventListener) {
         this.eventListener = eventListener;
         // report initial status to Unity
         // ...
      }
      private LiveWallpaperListener eventListener;
   }

When the Unity instance is initialized in Java by ``LiveWallpaperManager``, the C# part of UniLWP, ``LiveWallpaperManagerDroid`` will be awaken along with the Unity instance, and before any scene loading, it will call ``setEventListener(LiveWallpaperListener eventListener)`` with a C# `AndroidJavaProxy <https://docs.unity3d.com/ScriptReference/AndroidJavaProxy.html>`_. Any Android native events would be synced through this interface and dispatched to any listener attached.

It is also suggested that you attach listeners in Monobehavior's ``Start()`` or ``Awake()`` function to only register once after the internal setup of ``LiveWallpaperManagerDroid``.

Behaviour & Flags
^^^^^^^^^^^^^^^^^

UniLWP comes with a handful options to tweak its native behavior. Certain times you want UniLWP to log in detail, other times you don't. The same applies to Unity initialization, initial variable value, setting button event, etc. All those fields are organized into a single Java class ``LiveWallpaperConfig``, and the values would be retrieved from ``meta-data`` tags in the merged final ``AndroidManifest.xml``.

.. Tip:: For how to set behaviour flags in your C# code, please refer to :doc:`../tutorial/callbacks`

Android Module
--------------

The Android Module here refers to the ``unilwp.customize.androidlib`` folder located in ``Assets/FinGameWorks/UniLWP/Droid/Plugins`` folder. It is essentially an Android Library project, with the extension ``androidlib`` to identify itself as a plugin to Unity.

.. Note:: The ``androidlib`` extension is an Unity 2020.x feature addition that, if applied, can make your plugin folder work anywhere. In other words, plugins folders with or without this extension will work if placed in the ``Assets/Plugins/Android`` folder, however, on 2020+ and with this extension, the plugin folder can be moved to anywhere within ``Assets``.

In this sense, the Android Module will still largely work on 2019.3 if you move it into the global folder ``Assets/Plugins/Android``, but that is pretty in contrast with the 'non-invasive' design philosophy of UniLWP. If you really need it to work on 2019.3, please also modify the plugin path field in setting scripts so the editor UI will point to the correct file, but it won't receive offical support.

Resources
^^^^^^^^^

As described before, this folder is in a standard Android Library project layout. Aside from ``AndroidManifest.xml``, values are mostly stored in ``res/xml`` and ``res/values`` folder. In the final compile stage, these values will be merged into the app and replace any previous or default value.

Goal
^^^^

Why adding a new folder to the plugin folder when UniLWP already has an AAR file in it? Obviously AAR file cannot be modified easily after it is compiled. While the behavior can be redirected through ``meta-data`` entries mentioned earlier, all those resources files (names, images) are static-referenced.

An Android Library project that exposes its content to the outside is therefore more suitable to store these values. UniLWP since 0.0.2 comes with additional editor scripts to manage values within the editor so you don't have to use a xml editor or Android Studio.
