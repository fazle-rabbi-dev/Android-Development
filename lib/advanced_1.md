<h1 align="">Android Advanced ViewGropup/View (Part 1)</h1>


<p id="index"></p>

## Index Of Content

* [ListView & Array Adapter](#ArrayAdapter)
* [ListView & Base/Custom Adapter](#CustomAdapter)
* [GridView](#GridView)
* [Filtering & SearchView](#SearchView)
* [Menu](#Menu)
* [SearchView In Action Bar](#SearchViewInActionbar)
* [Gradient](#Gradient)
* [Spinner/Dropdown](#Spinner)
* [ProgressBar](#ProgressBar)
* [Fullscreen Activity](#Fullscreen)
* [Splash Screen Activity](#Splash)
* [Activity Name Changing](#ActivityNameChange)
* [Mediaplayer](#Mediaplayer)
* [Creating Share Menu](#Share)
* [Creating Feedback Menu](#Feedback)
* [AutoComplete TextView](#acTextView)
* [Expandable ListView](#Expandable)
* [Fragment](#Fragment)


<p id="ArrayAdapter"></p>

## ListView & Array Adapter
* ActivityMain.xml
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:orientation="vertical">
       <ListView
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:id="@+id/MyListViewId"/>
   </LinearLayout>
   ```
* Make sample_view.xml
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:orientation="vertical"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:padding="20dp">
   
	<TextView
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:text="Text"
		android:textColor="#FF16B88C"
		android:id="@+id/text"/>
   
   </LinearLayout>
   ```
* Make string array
   ```java
   <?xml version="1.0" encoding="utf-8"?>
   <resources>
       <string name="app_name">ADemo</string>
       
       <string-array name="fruits">
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
           <item>Apple</item>
       </string-array>
       
   </resources>
   ```
* MainActivity.java
   ```java
   public class MainActivity extends Activity { 
        
       private ListView MyListView;
     
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);
           
           MyListView = findViewById(R.id.MyListViewId);
           String[] fruits = getResources().getStringArray(R.array.fruits);
           ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,R.layout.sample_view,R.id.text,fruits);
           MyListView.setAdapter(adapter);
           
           
           // ListView Listener
           MyListView.setOnItemClickListener(new AdapterView.OnItemClickListener(){
                @Override
                public void onItemClick(AdapterView<?> p1, View p2, int p3, long p4) {
                    Toast.makeText(getApplicationContext(),"Okey",Toast.LENGTH_SHORT).show();
                } 
            });
        
       }
	
   } 
   
   ```

<a href="#index">⬆ Back to Top</a>

<p id="CustomAdapter"></p>

## ListView & Custom Adapter
* XML File
   ```xml
   <!--activity_main.xml-->
    <ListView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/MyListViewId"/>
        
   <!--sample_view.xml-->
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:orientation="vertical"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:padding="20dp">
   
	<TextView
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:text="Text"
		android:textColor="#FF16B88C"
		android:id="@+id/text"/>
   
	<TextView
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:text="Medium Text"
         android:textColor="#FFD14DE8"
		android:id="@+id/text2"/>
   
   </LinearLayout>
   
   ```
* MainActivity.java
   ```java
   public class MainActivity extends Activity { 
        
       private ListView MyListView;
     
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);
           
           MyListView = findViewById(R.id.MyListViewId);
           String[] fruits = getResources().getStringArray(R.array.fruits);
           String[] price = {"100","250","300","400","189","722","526","127","615","175"};
           
           //ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,R.layout.sample_view,R.id.text,fruits);
           CustomAdapter adapter = new CustomAdapter(this,fruits,price);
           
           
           MyListView.setAdapter(adapter);
           
       }
	
   } 
   
   ```

* CustomAdapter.java
   ```java
   public class CustomAdapter extends BaseAdapter {
       
       private String[] fruits;
       private String[] price;
       private Context context;
       LayoutInflater layoutInflater;
       
       CustomAdapter(Context context,String[] fruits,String[] price){
           this.fruits = fruits;
           this.price = price;
           this.context = context;
       }
       
       @Override
       public int getCount() {
           return fruits.length;
       }
   
       @Override
       public Object getItem(int p1) {
           return null;
       }
   
       @Override
       public long getItemId(int p1) {
           return 0;
       }
   
       @Override
       public View getView(int position, View convertView, ViewGroup parent) {
           
           
           layoutInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
           convertView = layoutInflater.inflate(R.layout.sample_view,parent,false);
           
           TextView fruits_name = convertView.findViewById(R.id.text);
           TextView fruits_price = convertView.findViewById(R.id.text2);
           
           fruits_name.setText(fruits[position]);
           fruits_price.setText(price[position]);
           
           return convertView;
       }
       
       
       
       
   }   
   ```

<a href="#index">⬆ Back to Top</a>

<a href="#index">⬆ Back to Top</a>

<p id="GridView"></p>

## GridView
* XML File
   ```xml
   <GridView
      android:id="@+id/MyGridViewId"
      android:layout_height="match_parent"
      android:layout_width="match_parent"
      android:numColumns="3"
      android:verticalSpacing="5dp"
      android:horizontalSpacing="5dp"
      android:listSelector="#f5d6ac"
      />
   ```
* Java File
   ```java
   // Use custom adapter same as ListView
   ```

<a href="#index">⬆ Back to Top</a>

<p id="SearchView"></p>

## SearchView
* XML File
   ```xml
   <SearchView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="10dp"
        android:id="@+id/searchView"
        android:hint="Search..."
    />
   ```
* Java File
   ```java
   // this will be work only for ArrayAdapter
   searchView.setOnQueryTextListener(new SearchView.OnQueryTextListener(){
   
       @Override
       public boolean onQueryTextSubmit(String p1) {
           return false;
       }
   
       @Override
       public boolean onQueryTextChange(String newText) {
           
           adapter.getFilter().filter(newText);
           
           return false;
       }
       
   
   });
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Menu"></p>

## Menu
* **Create--> layout/menu** folder
* create a xml file
* XML File
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <menu xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res/android"
   >
      <item
        android:id="@+id/item1"
        android:title="About"/>
      <item
        android:id="@+id/item2"
        android:title="Share"
        app:showAsAction="always"
        android:icon="@drawable/ic_share_variant_outline"
        app:iconTint="#ededed"
        />
      
      <item
        android:id="@+id/item3"
        android:title="Rating"/>
      
      <item
        android:id="@+id/item4"
        android:title="Follow Developer"
        
        />
   </menu>
   ```
* Java File
   ```java
   @Override
   public boolean onCreateOptionsMenu(Menu menu) {
     
     MenuInflater inflater = getMenuInflater();
     inflater.inflate(R.menu.option_menu,menu);
     return super.onCreateOptionsMenu(menu);
   }
   
   // Add Listener
   @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        
        if(item.getItemId() == R.id.item1){
            Toast.makeText(getApplicationContext(),"About Clicked",Toast.LENGTH_SHORT).show();
        }
        
        return super.onOptionsItemSelected(item);
    }
   ```

<a href="#index">⬆ Back to Top</a>

<p id="SearchViewInActionbar"></p>

## SearchView In Action Bar
* XML File
   ```xml
   <item
     android:id="@+id/searchId"        
     app:showAsAction="always"
     android:icon="@drawable/ic_share_variant_outline"
     app:iconTint="#ededed"
     app:actionViewClass="android.widget.SearchView"
     />
   ```
* Java File
   ```java
   @Override
   public boolean onCreateOptionsMenu(Menu menu) {
     
     // getting inflater object
     MenuInflater inflater = getMenuInflater();
     // creating option menu
     inflater.inflate(R.menu.option_menu,menu);
     
     // getting menu item
     menuItem = menu.findItem(R.id.searchId);
     // getting/finding type of item or actual item
     SearchView searchView = (SearchView) menuItem.getActionView();
     
     // Now i can add listener in searchview
     
     return super.onCreateOptionsMenu(menu);
   }
   
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Gradient"></p>

## Gradient
* Make a xml file in the drawable folder
* Then paste the bellow code
* Then use this as a Background coloe
* XML File
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   
   <shape xmlns:android="http://schemas.android.com/apk/res/android" android:shape="rectangle">
   
    <gradient
        android:type="linear"
        android:startColor="#784beb"
        android:endColor="#FF9278D6"
        android:centerColor="#FF2B1368"
        android:angle="0"
    />
   
   </shape>
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Spinner"></p>

## Spinner/Dropdown
* XML File
   ```xml
   <Spinner
      android:layout_height="wrap_content"
      android:layout_width="match_parent"
      android:layout_margin="10dp"
      android:id="@+id/MySpinnerId"/>
   ```
* Java File
   ```java
   public class MainActivity extends Activity { 
     
    private Spinner MySpinner;
    //private String[] myFavTechnology;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        MySpinner = findViewById(R.id.MySpinnerId);
        String[] myFavTechnology = {"C","Python","Java","Javascript","Rect Native","Nodejs","Expressjs","Flask"};
        
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,android.R.layout.simple_spinner_item,myFavTechnology);
        MySpinner.setAdapter(adapter);
        
        MySpinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener(){

                @Override
                public void onItemSelected(AdapterView<?> p1, View item, int index, long p4) {
                    // This method are used in button click listener
                    //MySpinner.getSelectedItem();
                    
                    // 
                    // myFavTechnology[index]
                    
                    Toast.makeText(getApplicationContext(),"Selected: "+MySpinner.getSelectedItem(),Toast.LENGTH_SHORT).show();
                }

                @Override
                public void onNothingSelected(AdapterView<?> p1) {
                }
                
            
        });
    }

  }

   ```

<a href="#index">⬆ Back to Top</a>

<p id="ProgressBar"></p>

## ProgressBar
* XML File
   ```xml
   <ProgressBar
        android:id="@+id/progress_bar"
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:max="100"
        android:progress="0"
        android:indeterminate="false"
        android:progressBackgroundTint="#FFD1CFCF"
        android:progressTint="#f53d87"
    />
   ```
* Java File
   ```java
   public class MainActivity extends Activity { 
     
    private ProgressBar progressBar;
    private int progress;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        progressBar = findViewById(R.id.progress_bar);
        
        Thread thread = new Thread(new Runnable(){

                @Override
                public void run() {
                    
                    for(progress=10;progress<=100;progress=progress+10){
                       try {
                           Thread.sleep(1000);
                           progressBar.setProgress(progress);
                       } catch (InterruptedException e) {
                           
                       }
                       
                   }
                    

                }
                
            
        });
        
        thread.start();
        
    }

  }

   ```

<a href="#index">⬆ Back to Top</a>

<p id="Fullscreen"></p>

## Fullscreen Activity
* Java File
   ```java
   requestWindowFeature(Window.FEATURE_NO_TITLE);
   getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
                           WindowManager.LayoutParams.FLAG_FULLSCREEN
                           );
   // then
   setContentView(R.layout.activity_main);
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Splash"></p>

## Splash Screen Activity
* Create a new Activity 
* Then add this Activity as launcher Activity in `manifest.xml`
* **For remove white blank screen**
* Add the bellow code in `manifest.xml` (SplashScreen Activity)
   ```xml
   android:theme="@style/SplashTheme"
   ```
* Add this in **style.xml**
   ```xml
   <style name="SplashTheme" parent="@android:style/Theme.Holo.Light.NoActionBar">
     --> for disable
     <!--<item name="android:windowDisablePreview">true</item>-->
     --> for change style
     <item name="android:windowBackground">@drawable/background_splash</item>
   </style>
   ```

<a href="#index">⬆ Back to Top</a>

<p id="ActivityNameChange"></p>

## Activity Name Changing
* Java File
   ```java
   this.setTitle("My Application");           
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Mediaplayer"></p>

## Mediaplayer
   ```java
   public class MainActivity extends Activity { 
     
    private Button playBtn;    
    private MediaPlayer mp;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        /*requestWindowFeature(Window.FEATURE_NO_TITLE);
        getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
                              WindowManager.LayoutParams.FLAG_FULLSCREEN
                    );*/
        
        this.setTitle("iMusic");                       
        setContentView(R.layout.activity_main);
        
        // Make mediaplayer object
        mp = MediaPlayer.create(getApplicationContext(),R.raw.song);
        
        playBtn = findViewById(R.id.playBtnId);
        playBtn.setOnClickListener(new View.OnClickListener(){
   
                @Override
                public void onClick(View p1) {
                    mp.start();
                    // there are many methods available:
                    //mp.pause();
                    //mp.seekTo(mp.getCurrentPosition()+1000);
                    // mp.getDuration();
                    
                }
                
            
        });
        
    }
   
    // when back button pressed this method will be called and music will be stop !
    @Override
    protected void onDestroy() {
        //super.onDestroy();
        if(mp.isPlaying()){
            mp.stop();
            mp.release();
            mp = null;
        }
    }
    
   }
   
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Share"></p>

## Share Menu
   ```java
   btn = findViewById(R.id.btn);
       btn.setOnClickListener(new View.OnClickListener(){

       @Override
       public void onClick(View view) {
           Intent share_intent = new Intent(Intent.ACTION_SEND);
           share_intent.setType("text/plain");
           String subject = "iMusic";
           String body = "Hello there this is an amzing music player android app by using this app you can listen music from your phone.";
           share_intent.putExtra(share_intent.EXTRA_SUBJECT,subject);
           share_intent.putExtra(share_intent.EXTRA_TITLE,"Share This App With Your Friends");
           share_intent.putExtra(share_intent.EXTRA_TEXT,body);
           startActivity(share_intent.createChooser(share_intent,"Share With"));
           
       }
                
            
   });
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Feedback"></p>

## Feedback Menu
   ```java
   btn = findViewById(R.id.btn);
   btn.setOnClickListener(new View.OnClickListener(){

       @Override
       public void onClick(View view) {
           Intent feedback_intent = new Intent(Intent.ACTION_SEND);
           feedback_intent.setType("text/plain");
           // get bellow data from user                    
           String[] email = {"test@gmail.com"};
           String subject = "iMusic";
           String body = "I found a bug in your app";
           
           feedback_intent.putExtra(feedback_intent.EXTRA_EMAIL,email);
           feedback_intent.putExtra(feedback_intent.EXTRA_SUBJECT,subject);
           feedback_intent.putExtra(feedback_intent.EXTRA_TEXT,body);
           
           startActivity(feedback_intent.createChooser(feedback_intent,"Feedback With"));
           
       }
                
            
   });
   ```

<a href="#index">⬆ Back to Top</a>

<p id="acTextView"></p>

## AutoComplete TextView
   ```java
   // in xml file:
   /*
   <AutoCompleteTextView
		android:id="@+id/acTextView"
		android:layout_height="wrap_content"
		android:layout_width="match_parent"/>
   */
   
   public class MainActivity extends Activity { 
     
    private AutoCompleteTextView acTextView;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        /*requestWindowFeature(Window.FEATURE_NO_TITLE);
        getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
                              WindowManager.LayoutParams.FLAG_FULLSCREEN
                    );*/
        
        this.setTitle("iMusic");                       
        setContentView(R.layout.activity_main);
        
        acTextView = findViewById(R.id.acTextView);
        String[] data = {"apple","banana","orange","android","bharot","chocolate","cupcake"};
        ArrayAdapter adapter = new ArrayAdapter(getApplicationContext(),android.R.layout.simple_list_item_1,data);
        // when one char type sujjestion will be appear
        acTextView.setThreshold(1);
        acTextView.setAdapter(adapter);
        
        acTextView.setOnItemClickListener(new AdapterView.OnItemClickListener(){

                @Override
                public void onItemClick(AdapterView<?> p1, View item, int index, long p4) {
                    Toast.makeText(getApplicationContext(),"Clicked on :"+index,Toast.LENGTH_SHORT).show();
                }
                
            
        });
        
    }
    
  }

   ```

<a href="#index">⬆ Back to Top</a>

<p id="Expandable"></p>

## Expandable ListView
* XML File
```xml

```
* Java File
```java

```

<p id="Fragment"></p>

## Fragment
   ```java
   
   ```

<a href="#index">⬆ Back to Top</a>


