<h2 align="center">Extra Concept</h2>

* [Hyperlink](#)
* [Change Actionbar Color](#)
* [Change Navigationbar Color](#)
* [Change Statusbar Color](#)
* [Button Styling](#Button)
* [Add Rounded Icon](#)
* [Copy Text](#Copy)
* [Pull Down Refresh](#Refresh)
* [Custom Header](#)
* [Get Network Info](#)
* [Pdf View](#)
* [Zoom Screen](#)
* [Document Picker](#)
* [File Download](#)
* [Runtime Permission](#Permission)

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

## Copy Text
```java
android.content.ClipboardManager clipboard = (android.content.ClipboardManager) getApplicationContext().getSystemService(Context.CLIPBOARD_SERVICE);
android.content.ClipData clip = android.content.ClipData.newPlainText("Copied Text", "rabbi");
clipboard.setPrimaryClip(clip);
```

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

## NavigationbarColor Change
* styles.xml
```xml
<item name="android:navigationBarColor">@color/primary</item>
```

[Back To Top](#index)

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

## 
```

```

[Back To Top](#index)

