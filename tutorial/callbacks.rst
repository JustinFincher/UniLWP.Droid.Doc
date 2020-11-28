Listen To Callbacks
===================

UniLWP.Droid provides callbacks for developers to register in C# so they can respond to Android native events.

Callback Types And Registration
----------------------------------

| Currently, all available callbacks are declared within ``LiveWallpaperManagerDroid``, a ``ScriptableObject`` singleton that you can access via a global variable.
| ``LiveWallpaperManagerDroid`` would be initialized prior to scene loading, so you can safely call ``LiveWallpaperManagerDroid.Instance`` in ``Awake()`` or ``Start()`` without worrying null reference exceptions.
| If you want to acquire the initial state of callback values, ``LiveWallpaperManagerDroid`` also has a set of static variables with corrsponding names to the callback methods as initial values. 
| Below is an example of how to acquire initial value of the screen status and also listen for future changes.

.. code-block:: csharp
   :linenos:
   :emphasize-lines: 8,11

    using FinGameWorks.UniLWP.Droid.Scripts.Managers;

    public class Demo : MonoBehaviour
    {
    	private void Awake()
        {
            // acquire the initial screen status
            Enums.ScreenStatus screenStatus = LiveWallpaperManagerDroid.screenStatus;
            Debug.Log("ScreenStatus " + screenStatus);

            LiveWallpaperManagerDroid.Instance.screenDisplayStatusUpdated += status =>
            {
            	// triggered every time screen status has change
            	Debug.Log("ScreenStatus " + status);
            };
        }
    }



Insets
^^^^^^

	Insets refer to `android.view.WindowInsets <https://developer.android.com/reference/android/view/WindowInsets>`_, a set of value describing the padding of android window where you should avoid drawing to. This is especially useful when you are trying to run Unity UI on Android devices with notches.

	.. rubric:: Called when

	When the app has entered an Actvitiy or a Wallpaper Service.

	.. rubric:: Value

	Padding values in pixel format. Please use in conjuntion with `Screen.width <https://docs.unity3d.com/ScriptReference/Screen-width.html>`_ to calucate the percentage if you are in a scaled UI space.

	.. code-block:: csharp
    		:caption: Declaration

     		public delegate void OnInsetsUpdatedDelegate(int left, int top, int right, int bottom);
        	public OnInsetsUpdatedDelegate insetsUpdated;
        	public static Vector4 insets;

	.. code-block:: csharp
    		:caption: Example

     		LiveWallpaperManagerDroid.Instance.insetsUpdated += (left, top, right, bottom) =>
     		{
     		};

Offsets
^^^^^^^
	Offsets refer to the distance the users have scrolled on their Android home (launcher). It is derived from the `WallpaperService.Engine#onOffsetsChanged <https://developer.android.com/reference/android/service/wallpaper/WallpaperService.Engine#onOffsetsChanged(float,%20float,%20float,%20float,%20int,%20int)>`_ method with slight modifications.

	.. rubric:: Called when

	When the user is swiping across pages on Android launchers.

	.. rubric:: Value

	- float xOffset: Wallpaper horizontal scoll progress in a 0-1 scale.
	- float yOffset: Wallpaper vertical scoll progress in 0-1 scale. Since there isn't much support of vertical launcher pages in Android apps, this value is mostly reportede as 0.
	- float xOffsetStep: The progress a horizontal full-page scroll would take in a 0-1 scale. Consequently, total horizontal page count can be calucated by 1 divided by this value ``(int)(1.0/xOffsetStep)``.
	- float yOffsetStep: The progress a vertical full-page scroll would take in a 0-1 scale.
	- bool simulated: Since certain stock launchers and ROMs do not follow the described behavior in Android documentation (specifically, Samsung's OneUI), the value UniLWP acquired from those devices are always 0 or 0.5, resulting in no way to know the total launcher pages and progress. To work around this limitation, UniLWP is designed to deploy a gesture recoginizer to manually calucate the estimated progress, and simulated field would be true in this case.

	.. code-block:: csharp
    		:caption: Declaration

     		public delegate void OnWallpaperOffsetsUpdatedDelegate(float xOffset, float yOffset, float xOffsetStep, float yOffsetStep, bool simulated);
        	public OnWallpaperOffsetsUpdatedDelegate wallpaperOffsetsUpdated;
        	public static Vector4 offset;
        	public static bool offsetSimulated;

	.. code-block:: csharp
    		:caption: Example

     		LiveWallpaperManagerDroid.Instance.wallpaperOffsetsUpdated += (xOffset, yOffset, xStep, yStep, simulated) =>
        	{
        	    int xPageCount = xStep == 0 ? 0 : (int) Math.Round(1.0 / xStep);
        	    float xPageProgress = xPageCount * xOffset;
        	};


Dark Mode
^^^^^^^^^
	Dark mode 

Screen Display Status
^^^^^^^^^^^^^^^^^^^^^
	Screen display status refers to the lock state of a phone. You can utlize this value to perform certian animations when the user lights up or unlocks the phone. 
	
	.. Note:: For Android 9.0, this callback also include an always on display (AOD) value if you put ``androidprv:supportAmbientMode="true"`` into ``wallpaper.xml``. However, since Android 10, this attribute is protected by a permission ``android.permission.AMBIENT_WALLPAPER``, which is a system only permission that you normally cannot request except you are compling the ROM youself (i.e. you are also one of Android OEM companies or custom ROM makers)

	.. rubric:: Called when

	When the user has turn on the screen in lock state / unlock the phone / lock the phone / leave the phone into always on display mode

	.. rubric:: Value	

	Enums.ScreenStatus, where:

	- LockedAndOff = 0
	- LockedAndAOD = 1
	- LockedAndOn = 2
	- Unlocked = 3

	.. code-block:: csharp
    		:caption: Declaration

     		public delegate void OnScreenDisplayStatusUpdatedDelegate(Enums.ScreenStatus screenStatus);
        	public OnScreenDisplayStatusUpdatedDelegate screenDisplayStatusUpdated;
        	public static Enums.ScreenStatus screenStatus;

	.. code-block:: csharp
    		:caption: Example

     		LiveWallpaperManagerDroid.Instance.screenDisplayStatusUpdated += status =>
     		{
     		};

In Activity
^^^^^^^^^^^
	This callback reflects if the Unity instance is currently displaying in an activity.
	
	.. Note:: Notice that, this callback only works in the scope of UniLWP's own provided activities. If you are writing a customized activity and also want the UniLWP to receive this event in the C# side, please register your activity (refer to the ``Trigger Callbacks In Your Own Implementation`` section)

In Service
^^^^^^^^^^
	This callback reflects if the Unity instance is currently displaying in wallpaper mode.

Trigger Callbacks In Your Own Implementation
--------------------------------------------