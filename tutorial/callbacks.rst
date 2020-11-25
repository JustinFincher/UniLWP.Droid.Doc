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

	Pixels

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
	Offsets refer to the

Dark Mode
^^^^^^^^^
	Dark mode 


Trigger Callbacks In Your Own Implementation
--------------------------------------------