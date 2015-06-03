A library that allows you to connect of Wi-Fi hotspots. 


Do you want to write a android app that can make Wi-Fi connections? "WifiManager", "WifiConfiguration"... I do not think it's a easy job. I have no idea why the Android team gives us so ugly an interface.

After digging into the android source code I got something finally.

This library is very easy to use:


**A short example:
```
final Intent intent = new Intent("com.farproc.wifi.connecter.action.CONNECT_OR_EDIT");
intent.putExtra("com.farproc.wifi.connecter.extra.HOTSPOT", scanResult);
startActivity(intent);
```**A long example:
```
import android.app.Activity;
import android.content.ActivityNotFoundException;
import android.content.Intent;
import android.net.Uri;
import android.net.wifi.ScanResult;
import android.widget.Toast;
...
...
private static void launchWifiConnecter(final Activity activity, final ScanResult hotspot) {
  final Intent intent = new Intent("com.farproc.wifi.connecter.action.CONNECT_OR_EDIT");
  intent.putExtra("com.farproc.wifi.connecter.extra.HOTSPOT", hotspot);
  try {
    activity.startActivity(intent);
  } catch(ActivityNotFoundException e) {
    // Wifi Connecter Library is not installed.
    Toast.makeText(activity, "Wifi Connecter is not installed.", Toast.LENGTH_LONG).show();
    downloadWifiConnecter(activity);
  }
}

private static void downloadWifiConnecter(final Activity activity) {
  Intent downloadIntent = new Intent(Intent.ACTION_VIEW)
    .setData(Uri.parse("market://details?id=com.farproc.wifi.connecter"));
  try {
    activity.startActivity(downloadIntent);
    Toast.makeText(activity, "Please install this app.", Toast.LENGTH_LONG).show();
  } catch (ActivityNotFoundException e) {
    // Market app is not available in this device.
    // Show download page of this project.
    try {
      downloadIntent.setData(Uri.parse("http://code.google.com/p/android-wifi-connecter/downloads/list"));
      activity.startActivity(downloadIntent);
      Toast.makeText(activity, "Please download the apk and install it manully.", Toast.LENGTH_LONG).show();
    } catch  (ActivityNotFoundException e2) {
      // Even the Browser app is not available!!!!!
      // Show a error message!
      Toast.makeText(activity, "Fatel error! No web browser app in your device!!!", Toast.LENGTH_LONG).show();
    }
  }
}
```
See [com.farproc.wifi.connecter.TestWifiScan](https://code.google.com/p/android-wifi-connecter/source/browse/src/com/farproc/wifi/connecter/TestWifiScan.java) for detailes.

[Market page of this app](https://market.android.com/details?id=com.farproc.wifi.connecter).

&lt;wiki:gadget url="http://android-wifi-connecter.googlecode.com/svn/gadgets/adsense.xml" width="480" border="0"/&gt;