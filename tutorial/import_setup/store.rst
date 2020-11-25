Store Version
=============


.. Note:: As Unity 2020.1 deprecated the Unity Asset Store web browser panel in favour of the package manager, you need to use package manager to import UniLWP.Droid on 2020.1+

.. sidebar:: Paid Version Import Guide

   .. rubric:: Where is the package manager

   .. figure:: /_static/img/menu_package_manager.jpg

    Package Manager is located under menu ``Window``. The menu bar would be at the top of the screen in macOS while at the top of the Unity window in Windows.

   .. rubric:: How to find asset store packages you bought before in package manager

   .. figure:: /_static/img/package_manager_my_assets.jpg

    Switch package scope at the top-left menu, then use the search field at the top-right to search your assets.

   .. rubric:: How to import asset store packages in package manager

   .. figure:: /_static/img/package_manager_unilwp_store_import.jpg

    Choose the asset at the left sidebar, then press ``download`` and then ``import`` buttons at the bottom-right.


The paid version, UniLWP.Droid.Store, is distributed on `Unity Asset Store <http://u3d.as/1QVw>`_ as a ``.unitypackage`` file.

Import On 2020.1 +
------------------

- Open package manager via menu ``Window/Package Manager``. 
- Switch package scope to ``Packages: My Assets`` and search ``UniLWP``
- Choose ``UniLWP.Droid - Unity Live Wallpaper For Android``, then download and import

Import On 2019.3 +
------------------

- Open asset store panel via menu ``Window/Asset Store``.
- Search for ``UniLWP`` in the newly opened web version of asset store.
- Choose ``UniLWP.Droid - Unity Live Wallpaper For Android``, then download and import

Setup
-----

- After import, find UniLWP settings in ``Project Settings``. 

	- On macOS, the ``Project Settings`` panel can be toggled by menu path ``Edit/Project Settings...``
	- On Windows,

- Go to ``Build Settings`` and adjust certain items:

  - In ``Player/Resolution and Presentation``, make sure that both ``Optimized Frame Pacing`` and ``Render Over Native UI`` are unchecked.
  - In ``Player/Other Settings``, make sure that both ``Mute Other Audio Sources`` and ``Filter Touches When Obscured`` are unchecked, the ``Minimal API Level`` is ``Android 7.0 Nougat (API Level 24)``. You might also want to change ``Graphics APIs`` to ``OpenGLES3`` only, but that is optional.

- Go to ``Audio Settings`` and adjust certain items:

  - Check ``Disable Unity Audio`` if you don't want your wallpaper to play sounds.



Build
-----

Please refer to :doc:`../export`.