<h2 align="center">Android Advanced Part Two</h2>

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
* [Tab Navigation](#Tab)
* [Recycler View](#Recycler)

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

<p id="CardView"></p>

## CardView
* **build.gradle**
   ```gradle
   implementation "com.android.support:cardView-v7:27.1.1"
   ```
* **activity_main.xml**

	<details>
	<summary>Expand</summary>
	
	```xml
	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:background="#FFFFFFFF"
		android:padding="20dp"
		android:orientation="vertical"
		android:weightSum="2">
	
		<LinearLayout
			android:orientation="horizontal"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:layout_weight="1.0"
			android:weightSum="2">
	
			
			<android.support.v7.widget.CardView
				android:layout_weight="1.0"
				android:layout_height="match_parent"
				android:layout_width="match_parent"
	      android:clickable="true"
	      android:foreground="?android:attr/selectableItemBackground"
	      android:gravity="center"
	      android:layout_margin="2dp"
	      android:id="@+id/card_c"
	      >
	        
	        <LinearLayout
	           android:layout_height="match_parent"
	           android:layout_width="match_parent"
	           android:gravity="center"
	           android:background="#ededed"
	           android:orientation="vertical"
	           >
	             <ImageView
	                android:layout_height="50dp"
	                android:layout_width="50dp"
	                android:src="@drawable/c"
	                android:background="@drawable/circle_purple_bg"
	                android:padding="10dp"
	                />
	             <View
	                android:layout_height="2dp"
	                android:layout_width="match_parent"
	                android:background="#584beb"
	                android:layout_margin="5dp"
	                
	                />
	             <TextView
	                android:layout_height="wrap_content"
	                android:layout_width="wrap_content"
	                android:text="C Programming"
	                android:textColor="#784beb"
	                android:textStyle="bold"
	                android:typeface="serif"
	                />
	           
	        </LinearLayout>
	      
			</android.support.v7.widget.CardView>
	    <android.support.v7.widget.CardView
	        android:layout_weight="1.0"
	        android:layout_height="match_parent"
	        android:layout_width="match_parent"
	        android:clickable="true"
	        android:foreground="?android:attr/selectableItemBackground"
	        android:gravity="center"
	        android:layout_margin="2dp"
	        android:id="@+id/card_java"
	     >
	
	        <LinearLayout
	           android:layout_height="match_parent"
	           android:layout_width="match_parent"
	           android:gravity="center"
	           android:background="#ededed"
	           android:orientation="vertical"
	        >
	           <ImageView
	              android:layout_height="50dp"
	              android:layout_width="50dp"
	              android:src="@drawable/java"
	              android:background="@drawable/circle_pink_bg"
	              android:padding="10dp"
	              
	           />
	           <View
	              android:layout_height="2dp"
	              android:layout_width="match_parent"
	              android:background="#FFED129D"
	              android:layout_margin="5dp"
	
	           />
	           <TextView
	              android:layout_height="wrap_content"
	              android:layout_width="wrap_content"
	              android:text="Java Programming"
	              android:textColor="#FFED129D"
	              android:textStyle="bold"
	              android:typeface="serif"
	           />
	
	        </LinearLayout>
	
	     </android.support.v7.widget.CardView>
	
		</LinearLayout>
	
		     
	</LinearLayout>
	
	```
	   
	</details>   

<a href="#index">⬆ Back to Top</a>


<p id="Fullscreen"></p>

## Make a specific sctivity to Fullscreen
   ```java
   // write this code after setContentView
   getActionBar().hide();
   ```

<a href="#index">⬆ Back to Top</a>


<p id="Drawer"></p>

## Navigation Drawer
* activity_main.xml
   ```xml
	<android.support.v4.widget.DrawerLayout
	   xmlns:android="http://schemas.android.com/apk/res/android"
	   xmlns:app="http://schemas.android.com/apk/res-auto"
	   xmlns:tools="http://schemas.android.com/tools"
	   android:layout_width="match_parent"
	   android:layout_height="match_parent"
	   id="@+id/drawerId"
	   tools:openDrawer="start"
	>
	
	   <android.support.v7.widget.Toolbar
	      android:id="@+id/toolbar"
	      android:layout_width="match_parent"
	      android:layout_height="?attr/actionBarSize"
	      app:popupTheme="@style/ThemeOverlay.AppCompat.Light"/>
	   
	
	   <android.support.design.widget.NavigationView
	      android:layout_width="wrap_content"
	      android:layout_height="match_parent"
	      id="@+id/navId"
	      app:menu="@menu/nav_layout"
	      android:layout_gravity="start"
	      app:headerLayout="@layout/nav_header"
	   >
	
	   </android.support.design.widget.NavigationView>
	
	</android.support.v4.widget.DrawerLayout>
   
   ```
* res/menu/nav_layout.xml
   ```xml
	<?xml version="1.0" encoding="utf-8"?>
	<menu xmlns:android="http://schemas.android.com/apk/res/android"
	   xmlns:tools="http://schemas.android.com/tools"
	   tools:showIn="navigation_view"
	>
	
	   <group android:checkableBehavior="single">
	
	      <item
	         android:id="@+id/homeId"
	         android:title="Home"
	         android:icon="@drawable/home"
	      />
	      <item
	         android:id="@+id/aboutId"
	         android:title="About"
	         android:icon="@drawable/about"
	
	      />
	
	      <item
	         android:id="@+id/contactId"
	         android:title="Contact"
	         android:icon="@drawable/contact"
	
	      />
	
	   </group>
	
	
	</menu>   
   ```
* res/layout/nav_header.xml
	```xml
	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:orientation="vertical"
		android:layout_width="match_parent"
		android:layout_height="150dp"
		android:background="#FF08939A"
		android:gravity="center">
	
		<TextView
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:text="Nav Header"
			android:textAppearance="?android:attr/textAppearanceLarge"/>
	
	</LinearLayout>
	
	```


<a href="#index">⬆ Back to Top</a>


<p id="Tab"></p>

## Tab Navigation
* build.gradle
```gradle
compile 'com.android.support:appcompat-v7:27.1.1'
compile 'com.android.support:design:27.1.1'
compile 'com.android.support:support-v4:27.1.1'
```
* activity_main.xml
   ```xml
   <android.support.design.widget.TabLayout
		android:layout_height="wrap_content"
		android:layout_width="match_parent"
		android:id="@+id/tabLayout"
		android:background="#FF56EEEE"
     android:layout_weight="2"
    >

	</android.support.design.widget.TabLayout>

   ```
* MainActivity.java
   ```java
   // make viewpager
   viewPager.setAdapter(adapter);
   tabLayout.setupWithViewPager(viewPager);
   ```

<a href="#index">⬆ Back to Top</a>


<p id="Recycler"></p>

## Recycler View
* build.gradle
	```gradle
	compile 'com.android.support:recyclerview-v7:27.1.1'
	```
* activity_main.xml
   ```xml
   <android.support.v7.widget.RecyclerView
     android:layout_height="match_parent"
     android:layout_width="match_parent"
     android:id="@+id/recyclerView"
    />
   ```
* **write string-array in strings.xml**
* **Make a sample layout**
* MainActivity.java
   ```java
	package com.mycompany.application;
	
	import android.os.Bundle;
	import android.support.v7.app.AppCompatActivity;
	import android.support.v7.widget.Toolbar;
	import android.support.v7.widget.RecyclerView;
	import android.support.v7.widget.LinearLayoutManager;
	import android.view.View;
	import android.widget.Toast;
	
	public class MainActivity extends AppCompatActivity {
	    private RecyclerView recyclerView; 
	    String[] country_names;
	    String[] country_details;
	    
	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
			
			    Toolbar toolbar=(Toolbar)findViewById(R.id.toolbar);
			    setSupportActionBar(toolbar);
	        
	        recyclerView = findViewById(R.id.recyclerView);
	        country_names = getResources().getStringArray(R.array.country_names);
	        country_details = getResources().getStringArray(R.array.country_desc);
	        
	        MyAdapter adapter = new MyAdapter(this,country_names,country_details);
	        recyclerView.setAdapter(adapter);
	        recyclerView.setLayoutManager(new LinearLayoutManager(this));
	        
	       adapter.setOnItemClickListener(new MyAdapter.ClickListener(){
	
	             @Override
	             public void onItemClick(int position, View view) {
	                Toast.makeText(getApplicationContext(),"Clicked: "+country_names[position],Toast.LENGTH_SHORT).show();
	             }
	                        
	        });
	        
	    }
	    
	}
   
   ```
* MyAdapter.java

	<details>
	<summary>Click To Expand</summary>
	
	```java
	package com.mycompany.application;
	import android.support.v7.widget.RecyclerView;
	import android.view.ViewGroup;
	import android.view.View;
	import android.content.Context;
	import android.view.LayoutInflater;
	import android.widget.TextView;
	
	public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {
	  
	   private Context context;
	   private String[] country_names;
	   private String[] country_details;
	   private static ClickListener clickListener;
	   
	   MyAdapter(Context context,String[] country_names,String[] country_details){
	      this.context = context;
	      this.country_names = country_names;
	      this.country_details = country_details;
	   }
	   
	   @Override
	   public MyViewHolder onCreateViewHolder(ViewGroup viewGroup, int p2) {
	      
	      LayoutInflater inflater = LayoutInflater.from(context);
	      View view =inflater.inflate(R.layout.sample_layout,viewGroup,false);
	      return new MyViewHolder(view);
	   }
	
	   @Override
	   public void onBindViewHolder(MyViewHolder myViewHolder, int i) {
	      myViewHolder.countryName.setText(country_names[i]);
	      myViewHolder.countryDetails.setText(country_details[i]);
	      
	      //myViewHolder.countryName.setText("Test");
	      //myViewHolder.countryDetails.setText("ok");
	      
	      
	   }
	
	   @Override
	   public int getItemCount(){
	      return country_names.length;
	   }
	   
	
	   class MyViewHolder extends RecyclerView.ViewHolder implements View.OnClickListener {
	     
	      TextView countryName,countryDetails;
	      
	      public MyViewHolder(View itemView){
	         super(itemView);
	         
	         countryName = itemView.findViewById(R.id.countryName);
	         countryDetails = itemView.findViewById(R.id.countryDetails);
	         
	         // set listener
	         itemView.setOnClickListener(this);
	      }
	      
	      @Override
	      public void onClick(View view) {
	         clickListener.onItemClick(getAdapterPosition(),view);
	      }      
	      
	   }
	    
	   public interface ClickListener{
	      void onItemClick(int position,View view);
	   }
	   
	   public void setOnItemClickListener(ClickListener clickListener){
	      MyAdapter.clickListener = clickListener;
	   }
	    
	}		
	```
	
	</details>



<a href="#index">⬆ Back to Top</a>


