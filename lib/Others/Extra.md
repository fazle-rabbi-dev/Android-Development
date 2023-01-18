<h2 align="center">Extra Topics</h2>

* [Hyperlink](#)
* [Change Actionbar Color](#)
* [Change Navigationbar Color](#)
* [Change Statusbar Color](#)
* [Add Rounded Icon](#)
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

