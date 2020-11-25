Structure
=========

After the import of the store (paid) version, you should have those files in the ``Assets/FinGameWorks`` folder:

.. tree -I '*.meta'

.. parsed-literal::

	.
	└── UniLWP
	    ├── Droid # Root folder for UniLWP.Droid.
	    │   ├── CHANGELOG.md
	    │   ├── Editor # Editor scripts, including settings panel, post-build scripts, etc.
	    │   │   ├── Scripts
	    │   │   │   ├── Datas
	    │   │   │   │   ├── AndroidManifestXml.cs
	    │   │   │   │   ├── AndroidResourceXml.cs
	    │   │   │   │   ├── AndroidWallpaperXml.cs
	    │   │   │   │   └── BuildPathInfo.cs
	    │   │   │   ├── Helpers
	    │   │   │   │   ├── FileUtils.cs
	    │   │   │   │   ├── ProjectUtils.cs
	    │   │   │   │   └── StringUtils.cs
	    │   │   │   ├── Settings
	    │   │   │   │   ├── AdsProvider.cs
	    │   │   │   │   ├── BehaviorProvider.cs
	    │   │   │   │   ├── BuildAdvancedProvider.cs
	    │   │   │   │   ├── BuildProvider.cs
	    │   │   │   │   ├── BuildSimpleProvider.cs
	    │   │   │   │   ├── MainProvider.cs
	    │   │   │   │   ├── PreferenceProvider.cs
	    │   │   │   │   ├── ResourcesProvider.cs
	    │   │   │   │   ├── ResourcesScreensaverProvider.cs
	    │   │   │   │   ├── ResourcesStringProvider.cs
	    │   │   │   │   ├── ResourcesWallpaperProvider.cs
	    │   │   │   │   ├── SimulatorProvider.cs
	    │   │   │   │   └── UtilsProvider.cs
	    │   │   │   └── Windows
	    │   │   │       └── MenuActions.cs
	    │   │   └── Settings
	    │   │       └── BuildPathInfo.asset
	    │   ├── JavaSource.zip # Java source files for the aar plugin
	    │   ├── Plugins
	    │   │   ├── UniLWP-debug.aar # The aar plugin
	    │   │   └── unilwp.customize.androidlib # The customization Android module that works on top of the aar plugin
	    │   │       ├── AndroidManifest.xml
	    │   │       ├── libs
	    │   │       ├── project.properties
	    │   │       └── res
	    │   │           ├── mipmap
	    │   │           │   └── unilwp_preview.jpg
	    │   │           ├── values
	    │   │           │   └── strings.xml
	    │   │           ├── xml
	    │   │           │   ├── unilwp_wallpaper.xml
	    │   │           │   └── unilwp_wallpaper_template.xml
	    │   │           ├── xml-v25
	    │   │           │   └── unilwp_wallpaper.xml
	    │   │           └── xml-v29
	    │   │               └── unilwp_wallpaper.xml
	    │   ├── README.md
	    │   ├── Resources
	    │   │   └── LiveWallpaper.Manager.Droid.asset # ScriptableObject Singleton for global Live Wallpaper Manager access
	    │   └── Scripts # Scripts that works in both editor and runtime
	    │       ├── Datas
	    │       │   └── Enums.cs
	    │       ├── Managers
	    │       │   ├── Fingleton.cs
	    │       │   ├── LiveWallpaperManagerDroid.cs
	    │       │   ├── LiveWallpaperMonoInjecterDroid.cs
	    │       │   └── Singleton.cs
	    │       └── UniLWP.cs
	    ├── Droid.Demo
	    │   ├── Materials
	    │   │   ├── Particle.mat
	    │   │   └── Trail.mat
	    │   ├── Scenes
	    │   │   └── Main.unity
	    │   └── Scripts
	    │       └── Controllers
	    │           └── UIController.cs
	    └── UniLWP.Droid\ Documentation.pdf

	27 directories, 46 files

