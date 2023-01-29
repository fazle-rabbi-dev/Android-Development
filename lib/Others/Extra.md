<h2 align="center">Extra Concept</h2>

* [Hyperlink](#Hyperlink)

* [Make Shape Background](#Shapebg)

* [Copy Text](#Copy)

* [Pull Down Refresh](#Refresh)

* [Change Navigationbar Color](#NavigationbarColor)

* [Button Styling](#Button)

* [Runtime Permission](#Permission)

* [Get Network Info](#NetworkInfo)

* [Get Device Info](#DeviceInfo)

* [Change Actionbar Color](#)

* [Change Statusbar Color](#)

* [Add Rounded Icon](#)

* [Custom Header](#)

* [Pdf View](#)

* [Zoom Screen](#)

* [Document Picker](#)

* [File Download](#)


# Question Link
* [When Keyboard Appear Layout Will Be Resize](https://stackoverflow.com/questions/16411056/how-to-adjust-layout-when-soft-keyboard-appears)

<p id="Hyperlink"></p>

## Hyperlink
* **Method 1**
	```xml
	<TextView
	   android:autoLink="all"
	   android:layout_width="wrap_content"
	   android:layout_height="wrap_content"
	   android:text=" Phone: +88018819*** \n   
					  Email: forvideoderapp@gmail.com \n
				      More Apps: https://play.google.com/store/apps/details?id=com.codewithharry.isangeet  "
	   android:id="@+id/myTextView"/>
	```
* **Method 2**
1. *activity_main.xml*
	```xml
	<TextView
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:text="@string/hyperlink"
			android:layout_margin="10dp"
			android:id="@+id/hyperlink"/>
	```
2. *Strings.xml*
	```xml
	<string name="hyperlink">Learn more about Android app development at\n<a href="https://learntodroid.com">LearnToDroid.com</a></string>
	```
3. *MainActivity.java*
	```java
	TextView linkTextView = findViewById(R.id.hyperlink);
   linkTextView.setMovementMethod(LinkMovementMethod.getInstance());
   linkTextView.setLinkTextColor(Color.RED);
	```
* **Method 3**
	```java
	// Using implecit intent
	
	@Override
	   public void onClick(View button) {
	      //Toast.makeText(getApplicationContext(),"Ok",Toast.LENGTH_LONG).show();
	      if(button.getId() == R.id.callBtn){
	         Toast.makeText(getApplicationContext(),"Ok",Toast.LENGTH_LONG).show();
	         Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("tel:+880177528177"));
	         startActivity(intent);
	      }
	      else if (button.getId() == R.id.linkBtn){
	         Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("https://cutt.ly/rabbi"));
	         startActivity(intent);
	      }
	      else if(button.getId() == R.id.follow){
	         Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("https://cutt.ly/rabbi"));
	         startActivity(intent);
	      }
	      else{
	         Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("geo:16 17 38,18 28 18"));
	         startActivity(intent);
	      }
	   }	
	```

<p id="Shapebg"></p>

## How To Make Shape Background
* Create a new file inside drawable `circle_pink_bg.xml`
	```xml
	<?xml version="1.0" encoding="utf-8"?>
	<shape
	   android:shape="oval"
	   xmlns:android="http://schemas.android.com/apk/res/android"
	>
	
	   <solid android:color="#FFED129D"></solid>
	
	</shape>	
	```

<p id="Copy"></p>

## Copy Text
```java
android.content.ClipboardManager clipboard = (android.content.ClipboardManager) getApplicationContext().getSystemService(Context.CLIPBOARD_SERVICE);
android.content.ClipData clip = android.content.ClipData.newPlainText("Copied Text", "rabbi");
clipboard.setPrimaryClip(clip);
```

<p id="Refresh"></p>

## Pull Down To Refresh
* build.gradle
```gradle
implementation "androidx.swiperefreshlayout:swiperefreshlayout:1.1.0"
```
* activity_main.xml
```xml
<androidx.swiperefreshlayout.widget.SwipeRefreshLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/swipeRefresh"
    >

    <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/text"
       android:text="Home Screen"
       />
    
</androidx.swiperefreshlayout.widget.SwipeRefreshLayout>
```
* MainActivity.java
```java
//make variable
private SwipeRefreshLayout swipeRefresh;
// find layout
swipeRefresh = findViewById(R.id.swipeRefresh);

	swipeRefresh.setColorSchemeColors(Color.BLUE, Color.RED, Color.GREEN);
	swipeRefresh.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener(){

    @Override
    public void onRefresh() {
       Toast.makeText(getApplicationContext(),"Refreshing",Toast.LENGTH_SHORT).show();
       
       Thread thread = new Thread(new Runnable(){

             @Override
             public void run() {
                try {
                   Thread.sleep(4000);
                   swipeRefresh.setRefreshing(false);
                } catch (InterruptedException e) {}
             }
             
          
       });
       
       thread.start();
       
    }
    
  
});

```

<p id="NavigationbarColor"></p>

<p id="NavigationbarColor"></p>

## NavigationbarColor Change
* styles.xml
```xml
<item name="android:navigationBarColor">@color/primary</item>
```

[Back To Top](#index)

<p id="Button"></p>

<p id="Button"></p>

## Button Styling
* make 3 resource file
* add `@drawable/button` as Background in `Button`
* button.xml
	```
	<?xml version="1.0" encoding="utf-8"?>
	<selector
	   xmlns:android="http://schemas.android.com/apk/res/android"
	   >
	   
	   <item android:state_pressed="false" android:drawable="@drawable/btn_normal"/>
	   <item android:state_pressed="true" android:drawable="@drawable/btn_hover"/>
	      
	</selector>
	
	```
* btn_normal.xml
	```
	<?xml version="1.0" encoding="utf-8"?>
	<shape
	   android:shape="rectangle"
	   xmlns:android="http://schemas.android.com/apk/res/android"
	>
	
	   <solid android:color="#FFED129D"></solid>
	   <corners android:radius="10dp"/>
	   <stroke android:width="3dp"
	           android:color="#ededed"
	      />
	   
	</shape>		
	```
* btn_hover.xml
	```
	<?xml version="1.0" encoding="utf-8"?>
	<shape
	   android:shape="rectangle"
	   xmlns:android="http://schemas.android.com/apk/res/android"
	>
	
	   <solid android:color="#FFB9107B"></solid>
	   <corners android:radius="10dp"/>
	   <stroke android:width="3dp"
	      android:color="#ededed"
	   />
	      
	</shape>		
	```

[Back To Top](#index)

<p id="Permission"></p>

<p id="Permission"></p>

## Runtime Permission
* Dependency
	```gradle
	implementation 'com.karumi:dexter:6.2.3'
	```
* MainActivity.java
	```java
	//Prompt For Access Storage
	Dexter.withContext(this)
          .withPermission(Manifest.permission.READ_EXTERNAL_STORAGE)
          .withListener(new PermissionListener(){

             @Override
             public void onPermissionGranted(PermissionGrantedResponse p1) {
                // Do something
             }

             @Override
             public void onPermissionDenied(PermissionDeniedResponse p1) {
             }

             @Override
             public void onPermissionRationaleShouldBeShown(PermissionRequest pRequest, PermissionToken pToken) {
                pToken.continuePermissionRequest();
             }
             
             
          })
          .check();
	```

[Back To Top](#index)

<p id=""></p>

<p id="NetworkInfo"></p>

## Get Network Info
* **CheckInternet.java**
	```java
	package com.rabbi.netinfo;
	import android.content.BroadcastReceiver;
	import android.content.Intent;
	import android.content.Context;
	import android.net.ConnectivityManager;
	import android.net.NetworkInfo;
	import android.app.AlertDialog;
	import android.widget.Toast;
	import android.content.DialogInterface;
	import android.view.LayoutInflater;
	import android.view.View;
	import android.widget.Button;
	
	
	public class CheckInternet extends BroadcastReceiver {
	   private AlertDialog noInternetDialog;
	   private boolean has_internet;
	   
	   @Override
	   public void onReceive(Context context, Intent intent) {
	      if (intent.getAction().equals(ConnectivityManager.CONNECTIVITY_ACTION)) {
	         ConnectivityManager cm = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
	         NetworkInfo activeNetwork = cm.getActiveNetworkInfo();
	         boolean isConnected = activeNetwork != null && activeNetwork.isConnectedOrConnecting();
	
	         if (!isConnected) {
	            // Show an alert dialog if there is no internet connectivity
	            //has_internet = false;   
	            //showNoInternetDialog(context);            
	            show_custom_alert(context);
	         } else if (noInternetDialog != null && noInternetDialog.isShowing()) {
	            // Dismiss the alert dialog if internet connectivity is restored
	            //has_internet = true;
	            noInternetDialog.dismiss();                        
	         }
	      }
	   }
	   
	   
	   // Show No Internet Alert Dialog
	   public void showNoInternetDialog(final Context context){
	      if(!has_internet){
	         AlertDialog.Builder alertDialog = new AlertDialog.Builder(context)
	         
	         .setTitle("No Internet")
	         .setMessage("Please check your internet connection")
	         .setCancelable(false)
	         .setPositiveButton("Retry", new DialogInterface.OnClickListener(){
	
	               @Override
	               public void onClick(DialogInterface p1, int p2) {
	                  if(!has_internet){
	                     showNoInternetDialog(context);
	                  }
	                  else{
	                     noInternetDialog.dismiss();
	                  }
	               }
	                           
	         })
	         ;
	         noInternetDialog = alertDialog.create();
	         noInternetDialog.show();
	      }      
	   }
	   
	   
	   // Show Custom Alert Dialog
	   public void show_custom_alert(final Context context){
	      LayoutInflater inflater = LayoutInflater.from(context);
	      View view = inflater.inflate(R.layout.no_internet_custom_alert,null);
	      AlertDialog.Builder ab = new AlertDialog.Builder(context);
	      ab.setView(view);
	      
	      Button retryBtn = view.findViewById(R.id.retryBtn);
	      retryBtn.setOnClickListener(new View.OnClickListener(){
	
	            @Override
	            public void onClick(View p1) {
	               if(!has_internet){
	                  noInternetDialog.dismiss();
	                  show_custom_alert(context);
	               }
	               else{
	                  noInternetDialog.dismiss();
	               }
	            }
	                     
	      });
	      
	      noInternetDialog = ab.create();
	      noInternetDialog.show();
	   }
	   
	   
	   
	}
	```
* **MainActivity.java**
	```java
	package com.rabbi.netinfo;
	import android.content.BroadcastReceiver;
	import android.content.Context;
	import android.content.Intent;
	import android.content.IntentFilter;
	import android.net.ConnectivityManager;
	import android.app.Activity;
	import android.app.AlertDialog;
	import android.os.Bundle;
	import android.net.NetworkInfo;
	import android.content.DialogInterface;
	import android.widget.Toast;
	
	
	public class MainActivity extends Activity {
	
	   private CheckInternet networkReceiver;   
	
	   @Override
	   protected void onCreate(Bundle savedInstanceState) {
	      super.onCreate(savedInstanceState);
	      setContentView(R.layout.activity_main);
	
	      // Create a broadcast receiver to listen for connectivity changes
	      
	      networkReceiver = new CheckInternet();      
	      
	      // Register the broadcast receiver
	      IntentFilter filter = new IntentFilter(ConnectivityManager.CONNECTIVITY_ACTION);
	      registerReceiver(networkReceiver, filter);
	      
	   }
	
	   
	   // UnRegister the broadcast receiver
	   @Override
	   protected void onDestroy() {
	      super.onDestroy();
	      unregisterReceiver(networkReceiver);
	   }
	                             
	}	
	```

[Back To Top](#index)

<p id="DeviceInfo"></p>

## Get Device Info
* For get `android id`
	```java
	String ID = Settings.Secure.getString(getContentResolver(),
	                                      Settings.Secure.ANDROID_ID);
	```
* For others information
* For `others` information
	```java
	import android.os.*;
	
	Build.MODEL
	Build...
	```

[Back To Top](#index)

## 
```

```

[Back To Top](#index)

