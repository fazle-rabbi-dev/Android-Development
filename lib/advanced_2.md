<h2 align="center">Android Advanced (Part 2)</h2>

<p id="index"></p>

* [Add Back Button In Actionbar](#BackButton)
* [Add Logo In Actionbar](#LogoInActionbar)
* [Applying Style Using styles.xml](#ApplyingStyle)
* `How to go another app activity`
* [Html content in WebView & TextView](#Html)
* [Scroll Tabs/ViewPager](#ViewPager)
* [CardView](#CardView)
* [Make Specific Activity Into Fullscreen Activity](#Fullscreen)
* [Navigation Drawer](#Navigation)
* [Tab Drawer](#Tab)
* [Create Modal](#Modal)


<p id="BackButton"></p>

## Adding Back Button
* Add this code inside the `onCreate()` method
   ```java
   getActionBar().setDisplayHomeAsUpEnabled(true);
   // for set listener
   @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        if(item.getItemId() == android.R.id.home){
            finish();
        }
        return super.onOptionsItemSelected(item);
    }
    
   ```
* **Another way** add this code in `manifest.xml` inside activity opening tag
   ```xml
   android:parentActivityName=".MainActivity"
   ```

<a href="#index">⬆ Back to Top</a>


<p id="LogoInActionbar"></p>

## Add Logo In Actionbar
* 
   ```java
   getActionBar().setDisplayShowHomeEnabled(true);
   getActionBar().setLogo(R.drawable.ic_share_variant_outline);
   getActionBar().setDisplayUseLogoEnabled(true);
   ```

<a href="#index">⬆ Back to Top</a>


<p id="ApplyingStyle"></p>

## Applying Style
* Create style in `styles.xml`
   ```xml
   <style name="btnPrimary" parent="@android:style/Widget.EditText">
        <item name="android:background">#784beb</item>
        <item name="android:textSize">27sp</item>
    </style>
    
    <style name="btnPrimary.btnDanger">
        <item name="android:background">#FF12C5B7</item>
    </style>
   ```
* Implement style in `textView`
   ```xml
   <Button
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:text="Termux Tutorial"
		android:id="@+id/btn"
		style="@style/btnPrimary"
		android:textColor="#FFFFFFFF"/>


    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Termux Tutorial"
        android:id="@+id/btn"
        style="@style/btnPrimary.btnDanger"
        android:textColor="#FFFFFFFF"/>
   ```


<a href="#index">⬆ Back to Top</a>


<p id="Html"></p>

## Html content in WebView & TextView
* 
   ```java
	public class MainActivity extends Activity { 
	    
	    private TextView textView;
	    private WebView webView;
	
	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	        
	        textView = findViewById(R.id.text);
	        webView = findViewById(R.id.webView);
	        
	        String myText = "<h1>Im Heading One</h1>";
	        textView.setText(Html.fromHtml(myText));
	        
	        webView.loadDataWithBaseURL(null,myText,"text/html","utf-8",null);
	        
	    }
		
	} 
   
   ```

<a href="#index">⬆ Back to Top</a>


<p id="ViewPager"></p>

## Scroll Tabs
1. **Add the bellow line in** `build.gradle`
   ```gradle
   implementation 'com.android.support:support-v4:27.0.2'
   ```
2. **Make one or more fragment** (`java+xml` file)
	* FragmentOne.java
	```java
	package com.mycompany.application;
	import android.support.v4.app.Fragment;
	import android.view.LayoutInflater;
	import android.view.View;
	import android.os.Bundle;
	import android.view.ViewGroup;
	
	public class Fragment_One extends Fragment {
	
	   @Override
	   public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
	      //return super.onCreateView(inflater, container, savedInstanceState);
	      return inflater.inflate(R.layout.one_fragment,container,false);
	   }
	    
	    
	    
	}	
	```
	* one_fragment.xml
	```xml
	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:orientation="vertical"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:gravity="center"
		android:padding="20dp"
		android:background="#FFF3F2F2">
	
		<TextView
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:text="Hello There Im Fragment One"
			android:textSize="26sp"
			android:textStyle="bold"
			android:gravity="center"/>
	
	</LinearLayout>
	```

<a href="#index">⬆ Back to Top</a>

4. **Add the bellow code in** `activity_main.xml`
   ```xml
	<?xml version="1.0" encoding="utf-8"?>
	<android.support.v4.view.ViewPager
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:id="@+id/viewPager">
	
		<android.support.v4.view.PagerTitleStrip
		 android:layout_width="wrap_content"
		 android:layout_height="wrap_content"
	    android:background="#f53d87"
	    android:textColor="#ffffff"
	    android:padding="15dp"
	    android:textSize="17dp"
	    android:textStyle="bold"
	    >
	
		</android.support.v4.view.PagerTitleStrip>
	
	</android.support.v4.view.ViewPager>
   ```

<a href="#index">⬆ Back to Top</a>

5. **Add the bellow code in** `MainActivity.java`
   ```java
	package com.mycompany.application;
	 
	import android.app.Activity;
	import android.os.Bundle;
	import android.support.v4.view.ViewPager;
	import android.support.v4.app.FragmentStatePagerAdapter;
	import android.support.v4.app.FragmentManager;
	import android.support.v4.app.Fragment;
	import android.support.v4.app.FragmentActivity;
	
	public class MainActivity extends FragmentActivity { 
	   private ViewPager viewPager;
	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	        
	        viewPager = findViewById(R.id.viewPager);
	        FragmentManager fm = getSupportFragmentManager();
	        CustomAdapter adapter = new CustomAdapter(fm);
	        viewPager.setAdapter(adapter);
	    }
		
	} 
	
	class CustomAdapter extends FragmentStatePagerAdapter {
	
	   public CustomAdapter(FragmentManager fm){
	      super(fm);
	   }
	   
	   @Override
	   public int getCount() {
	      return 2;
	   }
	
	   @Override
	   public Fragment getItem(int p) {
	      Fragment fragment = null;
	      if(p == 0){
	         fragment = new Fragment_One();
	      }
	      else if(p == 1){
	         fragment = new Fragment_Two();
	      }
	      return fragment;
	   }
	
	   @Override
	   public CharSequence getPageTitle(int position) {
	      //return super.getPageTitle(position);
	      if(position == 0){
	         return "Messages";
	      }
	      else if(position == 1){
	         return "Chat";
	      }
	      return null;
	   }      
	   
	}   
   ```

<a href="#index">⬆ Back to Top</a>


<p id="Fullscreen"></p>

## Make a specific sctivity to Fullscreen
   ```java
   // write this code after setContentView
   getActionBar().hide();
   ```

<a href="#index">⬆ Back to Top</a>


<p id=""></p>

## 
* 
   ```xml
   
   ```
* 
   ```java
   
   ```

<a href="#index">⬆ Back to Top</a>


