<a href="#"><h2 align="center">Android Advanced (Part 2)</h2></a>

<p id="index"></p>

## Index Of Content
* [Add Back Button In Actionbar](#)
* [Add Logo In Actionbar](#)
* [Applying Style Using styles.xml](#)
* `How to go another app activity`
* [Html content in WebView & TextView](#)
* [Scroll Tabs](#)
* [CardView](#)
* [Make Fullscreen Activity](#)
* [Navigation Drawer](#)
* [](#)
* [](#)


<p id=""></p>

## 
* 
```xml

```
* 
```java

```

<a href="#index">⬆ Back to Top</a>


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


<p id=""></p>

## 
* 
   ```xml
   
   ```
* 
   ```java
   
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


