# Splash Screen Right Way on Android!

![](https://raw.githubusercontent.com/Hacybeyker/SplashRightWay/master/resources/splash.gif)
###### This is the correct way to create a splash on android by doing 3 easy steps

# Step 1
Create a xml file in **drawable/splash.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@color/colorPrimaryDark" />
    <item>
        <bitmap
            android:gravity="center"
            android:src="@drawable/cyclop" />
    </item>
</layer-list>
```

# Step 2
Add this code in **values/styles.xml**

```xml
    ...
    
    <style name="SplashTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="android:windowBackground">@drawable/splash</item>
        <item name="windowNoTitle">true</item>
        <item name="windowActionBar">false</item>
        <item name="android:windowFullscreen">true</item>
        <item name="android:windowContentOverlay">@null</item>
    </style>
```

# Step 3
Create activity class **SplashActivity** without check in "Generate Layout File"

![alt text](https://github.com/Hacybeyker/SplashRightWay/blob/master/resources/SplashActivity.PNG?raw=true)

```kotlin
package com.hacybeyker.splashrightway

import android.content.Intent
import android.os.Bundle
import android.os.Handler
import androidx.appcompat.app.AppCompatActivity

class SplashActivity : AppCompatActivity() {

    private var handler: Handler = Handler()
    private lateinit var runnable: Runnable

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        runnable = Runnable {
            if (!isFinishing) {
                startActivity(Intent(this@SplashActivity, MainActivity::class.java))
                finish()
            }
        }
    }

    override fun onResume() {
        super.onResume()
        handler.postDelayed(runnable, 1500)
    }

    override fun onPause() {
        super.onPause()
        handler.removeCallbacks(runnable)
    }
}
```

###### Note that '1500' is the time it takes for the transition from SplashActivity to MainActivity.
###### The time is defined in milliseconds, so in this example the waiting time is 1.5 seconds.



