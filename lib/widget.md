<h1 align="center">Android Widget</h1>

* [TextView](#)
* [ScrollView](#)
* [Button](#)
* [ImageButton](#)
* [ImageView](#)
* [Toast](#)
* [Custom Toast](#)
* [EditText](#)
* [CheckBox](#)
* [RadioButton,RadioGroup](#)
* [Switch](#)
* [Seekbar](#)
* [RatingBar](#)
* [WebView](#)
* [DatePicker](#)
* [DatePicker Dialog](#)
* [TimePicker Dialog](#)
* [Analog Clock](#)
* [Digital Clock](#)
* [Alert Dialog](#)
* `Custom Alert Dialog`
* [VideoView](#)
* [ZoomControlls](#)
* [Layout Weight & WeightSum](#)
* [Custom Font](#)
* [Styling](#)


<p id="TextView"></p>

## TextView
```xml
<TextView
		android:text="@string/hello_world"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:textAllCaps="false"
		android:id="@+id/myText"
		android:gravity="center"/>

```

<p id="ScrollView"></p>


<p id="ScrollView"></p>

## ScrollView
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:gravity="top|center"
	android:padding="10dp">

	<ScrollView
		android:layout_height="match_parent"
		android:layout_width="match_parent"
		android:orientation="vertical"
	  >
	  <LinearLayout
	      android:layout_height="match_parent"
		  android:layout_width="match_parent"
		>
		
		<TextView
			android:text="@string/text"
		    android:layout_height="wrap_content"
		    android:layout_width="wrap_content"
		  />
		
	  </LinearLayout>
	</ScrollView>
	
</LinearLayout>
```

<p id="TextView"></p>

<p id="Button"></p>

## Button
* XML File:
```xml
<Button
		android:background="#226EDF"
		android:textColor="#FFFFFF"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:id="@+id/btn"
		android:text="Touch Me"/>
		
<!--For Add Icon-->
android:drawableLeft="@drawable/ic_launcher"
```
* Add Listener (Method 1):
```java
public class MainActivity extends Activity 
{
   private Button btn;
    
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
		
		btn = findViewById(R.id.btn);
		
	    btn.setOnClickListener(new View.OnClickListener(){

			 @Override
			 public void onClick(View element)
			 {
				btn.setText("Im Changed !");
			 }
		});
    }
}
```
* Add Listener (Method 2):
```java
public class MainActivity extends Activity implements OnClickListener
{
   private Button btn;
    
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
		
		btn = findViewById(R.id.btn);
		
	    btn.setOnClickListener(this);
    }

	@Override
	public void onClick(View p1)
	{
	   btn.setText("Im Changed !");
	}
}
```

<p id="ImageButton"></p>

## ImageButton
```xml
<ImageButton
		android:src="@drawable/ic_launcher"
		android:layout_height="wrap_content"
		android:layout_width="match_parent"
		android:background="#E5574E"/>

```

<p id="ImageView"></p>

## ImageView
```xml
<ImageView
		android:src="@drawable/fazle-rabbi"
		android:scaleType="fitStart"/>
```

<p id="EditText"></p>

<p id="Toast"></p>

## Toast
```java
// method 1
Toast.makeText(getApplicationContext(),"Okey",Toast.LENGTH_SHORT).show();
// method 2 (Changing position)
Toast toast = Toast.makeText(getApplicationContext(),"Okey",Toast.LENGTH_SHORT);
toast.setGravity(Gravity.CENTER,0,0);
toast.show();

```

<p id="CustomToast"></p>

## Custom Toast
```java
LayoutInflater inflater = getLayoutInflater();
// converting xml --> view
View customView = inflater.inflate(R.layout.custom_toast,(ViewGroup) findViewById(R.id.customToastId));

Toast toast = new Toast(getApplicationContext());
toast.setDuration(Toast.LENGTH_SHORT);
toast.setView(customView);
toast.show();
```

## EditText
```xml
<EditText
		android:layout_width="wrap_content"
		android:inputType="number"
		android:layout_height="wrap_content"
		android:ems="10"
		android:id="@+id/number"
		android:hint="Enter your phone number"
		android:backgroundTint="#F53D87"/>


<!--For Get Value In Java File-->
>> Find item
>> Then use:
>> item.getText()
```

<p id="CheckBox">CheckBox</p>

## CheckBox
* XML File
```xml
CheckBox
		android:text="I agree"
		android:id="@+id/myCheck"
		android:layout_height="wrap_content"
		android:layout_width="match_parent"/>
```
* Java File
```java
if(myCheck.isChecked()){
	   		text.setText(myCheck.getText());
	   }
```

<p id="RadioButton"></p>

## RadioGroup,RadioButton
```xml
<RadioGroup
		android:id="@+id/radioGroupId"
		android:layout_margin="10dp"
		android:padding="10dp"
		android:orientation="horizontal"
		android:layout_height="wrap_content"
		android:layout_width="match_parent"
		android:gravity="center">

		<RadioButton
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:text="Male"
			android:id="@+id/maleId"/>

		<RadioButton
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:text="Female"
			android:id="@+id/femaleId"/>

</RadioGroup>
```
* Java File
```java
@Override
	public void onClick(View p1)
	{
	   // At first --> find radioGroupId   		
	   // get selected radio button_id using radioGroupId
	   int id = radioGroupId.getCheckedRadioButtonId();
	   try{
		 // find selected button
	     Button genderButton = findViewById(id);
	     if(genderButton.getText().toString() != null){
	        // display selected button value
			Toast.makeText(getApplicationContext(),"Value:"+genderButton.getText(),Toast.LENGTH_SHORT).show();
	     }
	   }
	   catch(Exception e){
		  
	   }
	   
	}
```

<p id="Switch"></p>

## Switch
```java
MySwitch = findViewById(R.id.switchId);
MySwitch.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener(){

	 @Override
	 public void onCheckedChanged(CompoundButton buttonView, boolean isChecked)
	 {
		if(isChecked){
		   Toast.makeText(getApplicationContext(),"On",Toast.LENGTH_SHORT).show();
		}
		else{
		   Toast.makeText(getApplicationContext(),"Off",Toast.LENGTH_SHORT).show();
		}
	 }

});
```

<p id="Seekbar"></p>

## Seekbar
* XML File
```xml
<SeekBar
		android:layout_width="match_parent"
		android:id="@+id/mySeekbarId"
		android:layout_height="wrap_content"
		android:max="10"
		/>
```
* Java File
```java
mySeekBar = findViewById(R.id.mySeekbarId);
mySeekBar.setOnSeekBarChangeListener(new OnSeekBarChangeListener(){

	 @Override
	 public void onProgressChanged(SeekBar p1, int p2, boolean p3)
	 {
		Toast.makeText(getApplicationContext(),"Value: "+p2,Toast.LENGTH_SHORT).show();
	 }

	 @Override
	 public void onStartTrackingTouch(SeekBar p1)
	 {
		Toast.makeText(getApplicationContext(),"Start",Toast.LENGTH_SHORT).show();
	 }

	 @Override
	 public void onStopTrackingTouch(SeekBar p1)
	 {
		Toast.makeText(getApplicationContext(),"Stop",Toast.LENGTH_SHORT).show();
	 }
});
```


<p id="RatingBar"></p>

## RatingBar
* XML File
```xml
<RatingBar
		android:rating="2.0"
		android:numStars="5"
		android:stepSize="1"
		android:progressBackgroundTint="#ededed"
		android:progressTint="#CE92A3"
		android:layout_height="wrap_content"
		android:layout_width="wrap_content"
		android:id="@+id/ratingId"/>

```
* Java File
```java
myRatingBar = findViewById(R.id.ratingId);
// Initial Rating Value
Toast.makeText(getApplicationContext(),"Value: "+myRatingBar.getRating(),Toast.LENGTH_SHORT).show();
myRatingBar.setOnRatingBarChangeListener(new OnRatingBarChangeListener(){

	 @Override
	 public void onRatingChanged(RatingBar p1, float value, boolean p3)
	 {
		Toast.makeText(getApplicationContext(),"Value: "+value,Toast.LENGTH_SHORT).show();
	 }
});
```


<p id="WebView"></p>

## WebView
```java
// in xml:
<WebView/>

private WebView webView;

 @Override
 protected void onCreate(Bundle savedInstanceState)
 {
     super.onCreate(savedInstanceState);
     setContentView(R.layout.main);
	
    webView = findViewById(R.id.webView);
    WebSettings webSettings = webView.getSettings();
	// For javascript enable
    webSettings.setJavaScriptEnabled(true);
	// For open all url in app
	webView.setWebViewClient(new WebViewClient());
	webView.loadUrl("https://google.com");
 }

@Override
public void onBackPressed()
{
  if(webView.canGoBack()){
	 webView.goBack();
  }
  else{
	 super.onBackPressed();
  }
}
```


<p id="DatePicker"></p>

## DatePicker
```java
datePiker = findViewById(R.id.datePiker);
datePiker.getYear();
datePiker.getMonth();
datePiker.getDayOfMonth();
```


<p id="DatePickerDialog"></p>

## DatePicker Dialog
```java
public class MainActivity extends Activity implements OnClickListener
{

 private Button btn;
 private DatePicker datePiker;
 private DatePickerDialog datePickerDialog;
 private int day;
 private int month;
 private int year;

 @Override
 protected void onCreate(Bundle savedInstanceState)
 {
     super.onCreate(savedInstanceState);
     setContentView(R.layout.main);
	
   datePiker = new DatePicker(this);
   // the bellow variable's are (int) type
   year = datePiker.getYear();
   month = datePiker.getMonth();
   day = datePiker.getDayOfMonth();
	
   datePickerDialog = new DatePickerDialog(
			this,
			 new DatePickerDialog.OnDateSetListener(){

				@Override
				public void onDateSet(DatePicker p1, int Year, int Month, int Day)
				{
					Toast.makeText(getApplicationContext(),"Date :"+Day+"-"+Month+1+"-"+Year,Toast.LENGTH_SHORT).show();
				}
			},
			year,month,day
		);
		
   
   btn = findViewById(R.id.btn);
   btn.setOnClickListener(new View.OnClickListener(){

		 @Override
		 public void onClick(View p1)
		 {
		  	datePickerDialog.show();
		 }		  
   });
   
 }
```


<p id="TimePicker"></p>

## TimePicker
```xml
<TimePicker/>
```


<p id="TimePickerDialog"></p>

## TimePicker Dialog
```java
public class MainActivity extends Activity implements OnClickListener
{
 private Button btn;
 private TimePicker timePicker;
private int hour;
private int minute;
private TimePickerDialog timePickerDialog;

 @Override
 protected void onCreate(Bundle savedInstanceState)
 {
     super.onCreate(savedInstanceState);
     setContentView(R.layout.main);
	
	timePicker = new TimePicker(this);
    timePicker.setIs24HourView(false);
	hour = timePicker.getHour();
	minute = timePicker.getMinute();
	
    timePickerDialog = new TimePickerDialog(
			 this,
			 new TimePickerDialog.OnTimeSetListener(){
				@Override
				public void onTimeSet(TimePicker time, int Hour, int Minute)
				{
				   time.setIs24HourView(false);
				   Toast.makeText(getApplicationContext(),"Time: "+Hour+":"+Minute,Toast.LENGTH_SHORT).show();
				}				   
			},
			hour,minute,false
	);
	
	btn = findViewById(R.id.btn);
    btn.setOnClickListener(new View.OnClickListener(){
		 @Override
		 public void onClick(View p1)
		 {
			timePickerDialog.show();
		 }
	});
	
	
 }

```


<p id="Analog"></p>

## Analog Clock
```xml
<AnalogClock/>
```


<p id="Digital"></p>

## Digital Clock
```xml
<DigitalClock/>
```


<p id="Alert"></p>

## Alert Dialog
```java
public class MainActivity extends Activity
{
    
	private Button btn;
	AlertDialog.Builder adb;
	
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
		
		btn = findViewById(R.id.btn);
		
		adb = new AlertDialog.Builder(this);
		adb.setTitle("Warning");
		adb.setMessage("Are you sure you want to delete this message.You can't retrive message once deleted.");
		adb.setIcon(R.drawable.ic_launcher);
		
		// Set yes button
	    adb.setPositiveButton("Yes", new DialogInterface.OnClickListener(){
			 @Override
			 public void onClick(DialogInterface dialog, int which)
			 {
				Toast.makeText(getApplicationContext(),"Message deleted",Toast.LENGTH_SHORT).show();
			 }
		});
		
		// Set no button
	    adb.setNegativeButton("No", new DialogInterface.OnClickListener(){
			 @Override
			 public void onClick(DialogInterface dialog, int which)
			 {
				dialog.cancel();
			 }
		  });
		
		// set cancel button
	    adb.setNeutralButton("Cancel", new DialogInterface.OnClickListener(){
			 @Override
			 public void onClick(DialogInterface dialog, int which)
			 {
				Toast.makeText(getApplicationContext(),"Canceled",Toast.LENGTH_SHORT).show();
			 }
		  });
		  
		  
	    btn.setOnClickListener(new View.OnClickListener(){

			 @Override
			 public void onClick(View p1)
			 {
				AlertDialog alertDialog = adb.create();
				alertDialog.show();
			 }
		});
		
    }
	
 }
```


<p id="VideoView"></p>

## VideoView
```java
videoView = findViewById(R.id.videoView);
Uri uri = Uri.parse("android.resource://"+getPackageName()+"/"+R.raw.hack);
 
MediaController mc = new MediaController(this);

 skipBtn = findViewById(R.id.skipBtn);
skipBtn.setOnClickListener(new View.OnClickListener(){

	 @Override
	 public void onClick(View el)
	 {
		int p = videoView.getCurrentPosition();
		videoView.seekTo(p+10000);
		Toast.makeText(getApplicationContext(),"Skipped to 10 sec",Toast.LENGTH_SHORT).show();
	 }
});
```

<p id="ZoomControlls"></p>

## ZoomControlls
```xml

```

<p id="layoutWeight"></p>

## Layout WeightSum
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:gravity="top|center"
	android:padding="10dp"
	android:orientation="vertical"
	android:background="#292626"
	android:weightSum="5">

	<Button
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:text="Click Me"
		android:id="@+id/btn"
		android:background="#FFE100"
		android:layout_weight="1"
		android:layout_margin="10dp"/>

	<Button
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:text="Click Me"
		android:id="@+id/btn"
		android:background="#FFE100"
		android:layout_weight="1"
		android:layout_margin="10dp"/>

	<Button
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:text="Click Me"
		android:id="@+id/btn"
		android:background="#FFE100"
		android:layout_weight="1"
		android:layout_margin="10dp"/>
	  
  <Button
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:text="Click Me"
	android:id="@+id/btn"
	android:background="#FFE100"
	android:layout_weight="1"
	android:layout_margin="10dp"/>
  
  <Button
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:text="Click Me"
	android:id="@+id/btn"
	android:background="#FFE100"
	android:layout_weight="1"
	android:layout_margin="10dp"/>
	  

</LinearLayout>

```

<p id="font"></p>

## Custom Font
```java
text = findViewById(R.id.text);
myFont = Typeface.createFromAsset(getAssets(),"Baloo_2_regular.ttf");
text.setTypeface(myFont);
```
