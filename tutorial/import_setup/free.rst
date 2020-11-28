Free Version
============

.. sidebar:: Free Version Import Guide

   .. rubric:: Where is the package manager

   .. figure:: /_static/img/menu_package_manager.jpg

    Package Manager is located under menu ``Window``. The menu bar would be at the top of the screen in macOS while at the top of the Unity window in Windows.

   .. rubric:: How to add UPM packages

   .. figure:: /_static/img/package_manager_plus_sign.jpg

    If you cannot see the dropdown list, drag the title of package manager panel to un-dock the window, and then try again.

    .. rubric:: View more info about the package

    .. figure:: /_static/img/package_manager_load_unilwp.jpg

    Newly added files are groupped and shown within the ``Packages`` section of the project panel

    .. rubric:: Ideal project settings

    .. figure:: /_static/img/project_settings_player_resolution.jpg

    ``Project/Player/Resolution and Presentation``

    .. figure:: /_static/img/project_settings_player_other.jpg

    ``Project/Player/Other Settings``

Import
------

The free version, UniLWP.Droid.Free, is hosted on `GitHub <https://github.com/JustinFincher/UniLWP.Droid.Package.Free>`_ as an UPM package. 

- To import, first open package manager via menu ``Window/Package Manager``. 

- Then, at the top-left of the newly opened package manager window, you will find a plus sign. Click on it and select ``Add package from git URL...``

- Paste the following URL into the field and press enter:

   .. parsed-literal::

      https://github.com/JustinFincher/UniLWP.Droid.Package.Free.git

- Unity should download and load UniLWP.Droid as an UPM-formatted dependency.

Or, if you are familiar with ``package.json``, you are free to do paste this line into your json file:



.. code-block:: python
   :linenos:
   :emphasize-lines: 3

   "dependencies":
   {
      "com.justzht.unilwp.droid.free": "https://github.com/JustinFincher/UniLWP.Droid.Package.Free.git" // this line
   }

Setup
-----

Toggle ``Project Settings`` panel via menu path ``Edit/Project Settings...``

- Go to ``Project/Player`` and adjust certain items:

  - In ``Player/Resolution and Presentation``, make sure that both ``Optimized Frame Pacing`` and ``Render Over Native UI`` are unchecked.
  - In ``Player/Other Settings``, make sure that both ``Mute Other Audio Sources`` and ``Filter Touches When Obscured`` are unchecked, the ``Minimal API Level`` is ``Android 7.0 Nougat (API Level 24)``. You might also want to change ``Graphics APIs`` to ``OpenGLES3`` only, but that is optional.

- Go to ``Project/Audio`` and adjust certain items:

  - Check ``Disable Unity Audio`` if you don't want your wallpaper to play sounds.

Build
-----

It is the same as the default Unity build pipeline, that you only need to trigger a build through the default ``File/Build And Run`` menu path. The plugin will be packed into the final apk file and be initialized as soon as possible to handle Unity lifecycles.
