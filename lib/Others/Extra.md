<h2 align="center">Extra Topics</h2>

* [Hyperlink](#)
* [Change Actionbar Color](#)
* [Change Navigationbar Color](#)
* [Change Statusbar Color](#)
* [Add Rounded Icon](#)
* [How To Make Shape Background](#)
* [Add Border In Button](#)
* [Add Radius In Button](#)
* [Add Hover In Button](#)
* [Copy Text](#)
* [Api Calling](#)
* [Pull Down Refresh](#)
* [Custom Header](#)
* [Get Network Info](#)
* [Pdf View](#)
* [Zoom Screen](#)
* [](#)
* [](#)


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

