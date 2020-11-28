Ads
===

.. Warning:: Unity Ads support is experimental but it should work on 0.0.2 and up.

Ads support has two limitations for now:

- The ``Initial Activity Check Bypass`` flag should be enabled (The editor script will do this automatically)
- You can only show an ad in activity, not wallpaper.

.. sidebar:: Ads Settings

   .. rubric:: Before enabling Unity Ads support

   .. figure:: /_static/img/project_settings_unilwp_ads_disable.jpg

   .. rubric:: After enabling Unity Ads support

   .. figure:: /_static/img/project_settings_unilwp_ads_enable.jpg


To enable it, you need to:

- Go to the UniLWP Ad setting panel at ``Project Settings/UniLWP/Droid/Ads Integration``

- Click 'Activate' button. This step will:

    + Add ``UNILWP_ADS`` to your Android platform define symbols to enable certain blocks of code bound by ``#ifdef`` conditional compile flags

    + Set ``unilwp.behavior.activity.bypass.initial`` to true so that Unity Ads native library could acquire a proper context via ``UnityPlayer.currentActivity`` at startup.

- Click 'Unity Ads Settings' button to setup your ads and optionally add ads dependency.