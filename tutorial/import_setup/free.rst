Free Version
============

.. sidebar:: Free Version Import Guide

   .. rubric:: Where is the package manager

   .. figure:: /_static/img/menu_package_manager.jpg

    Package Manager is located under menu ``Window``. The menu bar would be at the top of the screen in macOS while at the top of the Unity window in Windows.

   .. rubric:: How to add UPM packages

   .. figure:: /_static/img/package_manager_plus_sign.jpg

    Package Manager is located under menu ``Window``. The menu bar would be at the top of the screen in macOS while at the top of the Unity window in Windows.

    .. rubric:: View more info about the package

    .. figure:: /_static/img/package_manager_load_unilwp.jpg

    If you 

The free version, UniLWP.Droid.Free, is hosted on GitHub as an UPM package. 

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