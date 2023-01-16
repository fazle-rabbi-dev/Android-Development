<a href="#"><h2 align="center">Android Advanced (Part 1)</h2></a>


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
1. Make a layout for header
2. Make a layout for header_details
* **activity_main.xml**
   ```xml
   <ExpandableListView
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:id="@+id/myListView"
		android:layout_margin="10dp"
		android:dividerHeight="10dp"
		android:divider="#FFFFFFFF"/>
   ```
* **MainActivity.java**
   ```java
   import ...
   
   public class MainActivity extends Activity { 
        
       private ExpandableListView myListView;
       private String[] headerData;
       private String[] detailsData;
       private ArrayList<String> header_data;
       private HashMap<String,ArrayList<String>> details_data;
       private int lastItem = -1;
       
       // For testing another data prepare way
       private ArrayList<String> my_header_data;
       private HashMap<String,ArrayList<String>> my_header_details;
       
       
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);
           
           // find listview
           myListView = findViewById(R.id.myListView);
           //prepareData();
           prepareData2();
           // make adapter and set adapter
           //CustomAdapter adapter = new CustomAdapter(this,header_data,details_data);
           //myListView.setAdapter(adapter);
           
           
           // For (prepareData2):
           CustomAdapter adapter = new CustomAdapter(this,header_data,details_data);
           myListView.setAdapter(adapter);
           
           
           // set listener
           myListView.setOnGroupClickListener(new ExpandableListView.OnGroupClickListener(){
   
                   @Override
                   public boolean onGroupClick(ExpandableListView p1, View view, int i, long p4) {
                       Toast.makeText(getApplicationContext(),header_data.get(i),Toast.LENGTH_SHORT).show();
                       return false;
                   }
                   
               
           });
           
           myListView.setOnGroupExpandListener(new ExpandableListView.OnGroupExpandListener(){
   
                   @Override
                   public void onGroupExpand(int index) {
                       if(lastItem != -1 && lastItem!= index){
                           myListView.collapseGroup(lastItem);
                       }
                       lastItem = index;
                       //Toast.makeText(getApplicationContext(),"Expanded",Toast.LENGTH_SHORT).show();
                   }
                   
               
           });
           
           myListView.setOnGroupCollapseListener(new ExpandableListView.OnGroupCollapseListener(){
   
                   @Override
                   public void onGroupCollapse(int index) {
                       
                       Toast.makeText(getApplicationContext(),"Collapsed",Toast.LENGTH_SHORT).show();
                   }
                   
               
           });
           
           myListView.setOnChildClickListener(new ExpandableListView.OnChildClickListener(){
   
                   @Override
                   public boolean onChildClick(ExpandableListView p1, View p2, int p3, int p4, long p5) {
                       Toast.makeText(getApplicationContext(),"Child clicked",Toast.LENGTH_SHORT).show();
                       return false;
                   }
                   
               
           });
           
       }
       
       // preparing data for expandable listView
       public void prepareData(){
           // getting data from xml
           headerData = getResources().getStringArray(R.array.header_data);
           detailsData = getResources().getStringArray(R.array.details_data);
           // initializing:
           header_data = new ArrayList<String>();
           details_data = new HashMap<>();
           
           for(int i=0;i<headerData.length;i++){
               header_data.add(headerData[i]);
               // make a new arraylist for add in the hashmap as value of key
               ArrayList<String> childData = new ArrayList<>();
               childData.add(detailsData[i]);
               
               // adding data in hashmap/object
               details_data.put(headerData[i],childData);
           }
           
       }
       
       
       // Another eay to preapare data 
       public void prepareData2(){
           header_data = new ArrayList<String>();
           details_data= new HashMap<>();
           
           header_data.add("1. Whwt is an api?");
           ArrayList<String> childData = new ArrayList<>();
           childData.add("1.1. Lorem ipsum");
           childData.add("1.2. Lorem ipsum");
           childData.add("1.3. Lorem ipsum");
           childData.add("1.4. Lorem ipsum");
           
           details_data.put(header_data.get(0),childData);
           
       }
       
	
   } 
   
   ```

<a href="#index">⬆ Back to Top</a>

* **CustomAdapter.java**
   ```java
   package ...
   import ...
   
   public class CustomAdapter extends BaseExpandableListAdapter {
   
       private Context context;
       private ArrayList<String> headerData;
       private HashMap<String,ArrayList<String>> detailsData;
       
       CustomAdapter(Context context,ArrayList<String> header_data,HashMap<String,ArrayList<String>> details_data){
           this.context = context;
           headerData = header_data;
           detailsData = details_data;
       }
       
       @Override
       public int getGroupCount() {
           return headerData.size();
       }
   
       @Override
       public int getChildrenCount(int p1) {
           return detailsData.get(headerData.get(p1)).size();
       }
   
       @Override
       public Object getGroup(int p1) {
           return headerData.get(p1);
       }
   
       @Override
       public Object getChild(int p1, int p2) {
           // p1 --> group position
           // p2 --> child position
           return detailsData.get(headerData.get(p1)).get(p2);
       }
   
       @Override
       public long getGroupId(int p1) {
           // group position
           return p1;
       }
   
       @Override
       public long getChildId(int p1, int p2) {
           // child position
           return p2;
       }
   
       // not needed
       @Override
       public boolean hasStableIds() {
           return false;
       }
   
       @Override
       public View getGroupView(int p1, boolean p2, View view, ViewGroup p4) {        
               String headerText = (String) getGroup(p1);
               if(view == null){
                   LayoutInflater inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
                   view = inflater.inflate(R.layout.header_layout,null);
               }
               TextView header_text= view.findViewById(R.id.header_text);
               header_text.setText(headerText);
           
           return view;
       }
   
       @Override
       public View getChildView(int p1, int p2, boolean p3, View view, ViewGroup p5) {
           String detailsText = (String) getChild(p1,p2);
           LayoutInflater inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
           view = inflater.inflate(R.layout.details_layout,null);
           TextView details_text= view.findViewById(R.id.details_text);
           details_text.setText(detailsText);
           
           return view;
       }
   
       // // not needed
       @Override
       public boolean isChildSelectable(int p1, int p2) {
           return true;
       }

   }   
   ```

<a href="#index">⬆ Back to Top</a>

<p id="Fragment"></p>

## Fragment
* activity_main.xml
   ```xml
	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:padding="0dp"
		android:weightSum="4"
		android:orientation="horizontal">
	
		<LinearLayout
			android:orientation="vertical"
			android:layout_width="0dp"
			android:layout_height="match_parent"
			android:layout_weight="2">
	
			<ListView
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				android:id="@+id/list_view"
				android:layout_margin="0dp"/>
	
		</LinearLayout>
	
		<LinearLayout
			android:orientation="vertical"
			android:layout_width="wrap_content"
			android:layout_height="match_parent"
			android:layout_weight="2">
	
			<fragment
				android:name="com.mycompany.application.SakibFragment"
				android:id="@+id/fragment_id"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
				android:layout_margin="0dp">
	
			</fragment>
	
		</LinearLayout>
	
	</LinearLayout>
   
   ```

<a href="#index">⬆ Back to Top</a>

* fragment_sakib.xml
   ```xml
	<?xml version="1.0" encoding="utf-8"?>
	<FrameLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:orientation="vertical"
		android:layout_width="match_parent"
		android:layout_height="match_parent"
		android:padding="10dp"
		android:background="#FF383933"
		android:layout_margin="20dp">
	
		<LinearLayout
			android:orientation="vertical"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:padding="20dp">
	
			<TextView
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:text="Name:Sakib"/>
	
			<TextView
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:text="Age:23"/>
	
		</LinearLayout>
	
	</FrameLayout>
   
   ```
* fragment_alamin.xml
   ```xml
   <!--Same as Previous-->
   ```

<a href="#index">⬆ Back to Top</a>

* SakibFragment.java
   ```java
	public class SakibFragment extends Fragment {
	
	    @Override
	    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
	        ///return super.onCreateView(inflater, container, savedInstanceState);
	        
	        return inflater.inflate(R.layout.fragment_sakib,container,false);
	        
	    }
	                
	}   
   ```
* AlaminFragment.java
   ```java
	public class SakibFragment extends Fragment {
	
	    @Override
	    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
	        ///return super.onCreateView(inflater, container, savedInstanceState);
	        
	        return inflater.inflate(R.layout.fragment_alamin,container,false);
	        
	    }
	                
	}   
   ```

<a href="#index">⬆ Back to Top</a>

* 
   ```java
	public class MainActivity extends Activity { 
	    
	    private ListView listView;
	    
	    
	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	        
	        listView= findViewById(R.id.list_view);
	        String[] person_names = {"Sakib","Alamin"};
	        ArrayAdapter adapter = new ArrayAdapter<String>(this,android.R.layout.simple_list_item_1,person_names);
	        listView.setAdapter(adapter);
	        
	        listView.setOnItemClickListener(new AdapterView.OnItemClickListener(){
	
	                @Override
	                public void onItemClick(AdapterView<?> p1, View view, int i, long p4) {
	                    Fragment fragment;
	                    
	                    if(i == 0){
	                        //sakib
	                        android.content.ClipboardManager clipboard = (android.content.ClipboardManager) getApplicationContext().getSystemService(Context.CLIPBOARD_SERVICE);
	                        android.content.ClipData clip = android.content.ClipData.newPlainText("Copied Text", "rabbi");
	                        clipboard.setPrimaryClip(clip);
	                        Toast.makeText(getApplicationContext(),"text copied",Toast.LENGTH_SHORT).show();
	                        fragment = new SakibFragment();
	                        FragmentManager fm = getFragmentManager();
	                        FragmentTransaction ft = fm.beginTransaction();
	                        ft.replace(R.id.fragment_id,fragment);
	                        ft.commit();
	                    }
	                    if(i == 1){
	                        // alamin
	                        fragment = new AlaminFragment();
	                        FragmentManager fm = getFragmentManager();
	                        FragmentTransaction ft = fm.beginTransaction();
	                        ft.replace(R.id.fragment_id,fragment);
	                        ft.commit();
	                    }
	                }
	                
	        });
	        
	    }
		
	} 
   
   ```

<a href="#index">⬆ Back to Top</a>


