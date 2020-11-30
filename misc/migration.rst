Migration
=========

0.0.2
-----

Issues worth noting from 0.0.0.1 to 0.0.2:

- The ``FinGameWorks/UniLWP/Droid`` menu items are grouped into sections for better readability. You can also use ``Project Settings/UniLWP/Droid`` panel which would provide the same functionality.
- Meta-data editing are now available directly within Editor (Unity 2020+).
- Changes of meta-data flags in UniLWP aar plugins:

    + ``unilwp.behavior.floating`` removed
    + ``unilwp.behavior.settings.notifyButton`` replaced by ``unilwp.style.activity.launch.display``
    + ``unilwp.behavior.resistToUpdate`` removed
    + ``unilwp.behavior.activity.expanded`` replaced by ``unilwp.behavior.preview.button.settings``
    + ``unilwp.behavior.lifecycle.resumeWithoutHolder`` replaced by ``unilwp.behavior.screen.off.early``
    + ``unilwp.behavior.activity.bypassCheck`` renamed to ``unilwp.behavior.activity.bypass.initial``
    + ``unilwp.ref.class.screensaver.service`` added
    + ``unilwp.ref.class.launcher.activity`` added
    + ``unilwp.ref.class.wallpaper.service`` added

- UniLWP.Droid now launches ``LiveWallpaperLauncherRedirectActivity`` instead of ``LiveWallpaperPresentationActivity``. ``LiveWallpaperLauncherRedirectActivity``, as you can guess from its name, is a launcher activity (meaning it adds an icon to your app drawer) to launch different activities depending on different configurations. Please refer to ``unilwp.style.activity.launch.display`` flag for different styles.