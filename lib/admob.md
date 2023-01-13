<h1 align="center">Admob Implementation</h1>

* ## NOTE:
* This implementation will be work on **AIDE.apk** and all the code are tested
* `Here are used admob sdk` **19.3.0**
* For **AIDE** you should use Exact this **19.3.0** version

<p id="Index"></p>

## Index
* [Setup App For Admob](#)
* [Banner Ad](#)
* [Interstitial Ad](#)
* [Rewarded Ad](#)


## At first you should follow the bellow instruction for implements every types of ads
* ### Step 1:
* Add Bellow Code In **app/build.gradle**
   ```gradle
   // Change This Version To 19
   minSdkVersion 19
   
   // add this under dependency
   implementation 'com.google.android.gms:play-services-ads:19.3.0'
   ```
* **All code look like:**
   ```gradle
   apply plugin: 'com.android.application'
   
   android {
       compileSdkVersion 21
       buildToolsVersion "21.1.0"
   
       defaultConfig {
           applicationId "com.mycompany.myapp2"
           minSdkVersion 19
           targetSdkVersion 29
           versionCode 1
           versionName "1.0"
       }
       buildTypes {
           release {
               minifyEnabled false
               proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
           }
       }
   }
   
   dependencies {
	  implementation 'com.google.android.gms:play-services-ads:19.3.0'
       compile fileTree(dir: 'libs', include: ['*.jar'])
   }   
   ```
* ### Step 2:
* Go to `AndroidManifest.xml`
* Add this code outside the `<application></application>`
   ```xml
   <uses-permission android:name="android.permission.INTERNET" />
   ```
* Add this code inside the `<application></application>`
   ```xml
   <!-- Sample AdMob app ID: ca-app-pub-3940256099942544~3347511713 -->
   <meta-data
   android:name="com.google.android.gms.ads.APPLICATION_ID"
   android:value="your_admob_app_id"/>
   ```

<a href="#index">⬆ Back to Top</a>


## NOTE
> **You can use all the code bellow in any xml & java file**

## Banner Ad
* **Step 1:** add this code in the ***activity_main.xml***
   ```xml
   <com.google.android.gms.ads.AdView
		xmlns:ads="http://schemas.android.com/apk/res-auto"
		android:id="@+id/adView"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:layout_centerHorizontal="true"
		android:layout_alignParentBottom="true"
		ads:adSize="BANNER"
		ads:adUnitId="your_banner_adUnit_id">
   </com.google.android.gms.ads.AdView>
   ```
* **Step 2:** open ***your MainActivity.java***
   * Add this code in the top
   ```java
   import com.google.android.gms.ads.*;
   import com.google.android.gms.ads.initialization.*;
   ```
   * Make a variable like this:
   ```java
   private AdView mAdView;
   ```
   * Add this code inside **onCreate()** method
   ```java
      MobileAds.initialize(this, new OnInitializationCompleteListener() {
			 @Override
			 public void onInitializationComplete(InitializationStatus initializationStatus) {
			 }
		  });
		
	   
	   mAdView = findViewById(R.id.adView);
	   AdRequest adRequest = new AdRequest.Builder().build();
	   mAdView.loadAd(adRequest);
	   
	   mAdView.setAdListener(new AdListener() {
			 @Override
			 public void onAdClicked() {
				// Code to be executed when the user clicks on an ad.
			 }

			 @Override
			 public void onAdClosed() {
				// Code to be executed when the user is about to return
				// to the app after tapping on an ad.
			 }

			 @Override
			 public void onAdFailedToLoad(LoadAdError adError) {
				// Code to be executed when an ad request fails.
			 }

			 @Override
			 public void onAdImpression() {
				// Code to be executed when an impression is recorded
				// for an ad.
			 }

			 @Override
			 public void onAdLoaded() {
				// Code to be executed when an ad finishes loading.
			 }

			 @Override
			 public void onAdOpened() {
				// Code to be executed when an ad opens an overlay that
				// covers the screen.
			 }
		  });   
   ```
   * Full Java File `look like:`
   <details>
      <summary>View Code</summary>
      
      ```java
      package com.mycompany.myapp2;
      import android.app.*;
      import android.content.*;
      import android.os.*;
      import android.view.*;
      import android.widget.*;
      import com.google.android.gms.ads.*;
      import com.google.android.gms.ads.initialization.*;
      
      
      
      public class MainActivity extends Activity 
      {
          private AdView mAdView;

          @Override
          protected void onCreate(Bundle savedInstanceState)
          {
              super.onCreate(savedInstanceState);
              setContentView(R.layout.main);
	
	   
	   MobileAds.initialize(this, new OnInitializationCompleteListener() {
			 @Override
			 public void onInitializationComplete(InitializationStatus initializationStatus) {
			 }
		  });
		
	   
	   mAdView = findViewById(R.id.adView);
	   AdRequest adRequest = new AdRequest.Builder().build();
	   mAdView.loadAd(adRequest);
	   
	   mAdView.setAdListener(new AdListener() {
			 @Override
			 public void onAdClicked() {
				// Code to be executed when the user clicks on an ad.
			 }
      
			 @Override
			 public void onAdClosed() {
				// Code to be executed when the user is about to return
				// to the app after tapping on an ad.
			 }
      
			 @Override
			 public void onAdFailedToLoad(LoadAdError adError) {
				// Code to be executed when an ad request fails.
			 }
      
			 @Override
			 public void onAdImpression() {
				// Code to be executed when an impression is recorded
				// for an ad.
			 }
      
			 @Override
			 public void onAdLoaded() {
				// Code to be executed when an ad finishes loading.
			 }
      
			 @Override
			 public void onAdOpened() {
				// Code to be executed when an ad opens an overlay that
				// covers the screen.
			 }
		  });
	   
          }
      }
      ```

   </details>

<a href="#index">⬆ Back to Top</a>


## Interstitial Ad
* Make a Button with id--> **btn** in the `xml` file for load ad when button will be clicked
* Make 2 Variable: One for `Button`, Second for `Interstitial Ad`
```java
package com.mycompany.myapp2;
import android.app.*;
import android.os.*;
import android.view.*;
import android.widget.*;
import com.google.android.gms.ads.*;
import com.google.android.gms.ads.initialization.*;


public class InterAd extends Activity
{

   private InterstitialAd mInterstitialAd;
   private Button btn;
   
   @Override
   protected void onCreate(Bundle savedInstanceState)
   {
	  // TODO: Implement this method
	  super.onCreate(savedInstanceState);
	  setContentView(R.layout.inter_ad);
	  
	  mInterstitialAd = new InterstitialAd(this);
	  mInterstitialAd.setAdUnitId("Interstitial_Ad_Unit_Id");
	  mInterstitialAd.loadAd(new AdRequest.Builder().build());
	  btn = findViewById(R.id.btn);
	  
	  btn.setOnClickListener(new View.OnClickListener(){

			@Override
			public void onClick(View item)
			{
			   if(mInterstitialAd.isLoaded()){
				  mInterstitialAd.show();
			   }
			   else{
				  mInterstitialAd.loadAd(new AdRequest.Builder().build());
			   }
			} 
	  });
	  
   }
   
}
```

<a href="#index">⬆ Back to Top</a>


## Rewarded Ad
* In the xml file make a Button with id `btn`
* Then go to java file and follow the bellow instruction
* Implements an interface like this:
   ```java
   implements RewardedVideoAdListener 
   ```
* After implements interface implements all the `abstract` method
* Make 2 Variable
   ```java
   private RewardedVideoAd mReward;
   private Button btn;
   ```
* Add this code inside `onCreate` method
   ```java
   mReward = MobileAds.getRewardedVideoAdInstance(this);
   mReward.loadAd("Rewarded_Ad_Unit_Id",new AdRequest.Builder().build());
   //loadVideoAd();
   
   btn = findViewById(R.id.btn);
   btn.setOnClickListener(new View.OnClickListener(){
	   @Override
	   public void onClick(View p1)
	   {
	     if(mReward.isLoaded()){
		    mReward.show();
	     }
	   }
   });
   ```
* **Full Java File Look Like This Code:**
   
   <details>
   <summary>View Code</summary>
   
   ```java
      package com.mycompany.myapp2;
      import android.app.*;
      import android.os.*;
      import android.view.*;
      import android.widget.*;
      import com.google.android.gms.ads.*;
      import com.google.android.gms.ads.reward.*;
      
      public class RewardAd extends Activity implements RewardedVideoAdListener    
      {
      
         @Override
         public void onRewardedVideoAdLoaded()
         {
	  // TODO: Implement this method
         }
      
         @Override
         public void onRewardedVideoAdOpened()
         {
	  // TODO: Implement this method
         }
      
         @Override
         public void onRewardedVideoStarted()
         {
	  // TODO: Implement this method
         }
      
         @Override
         public void onRewardedVideoAdClosed()
         {
	  // TODO: Implement this method
         }
      
         @Override
         public void onRewarded(RewardItem p1)
         {
	  // TODO: Implement this method
         }
      
         @Override
         public void onRewardedVideoAdLeftApplication()
         {
	  // TODO: Implement this method
         }
      
         @Override
         public void onRewardedVideoAdFailedToLoad(int p1)
         {
	  // TODO: Implement this method
         }
      
         @Override
         public void onRewardedVideoCompleted()
         {
	  // TODO: Implement this method
         }
         
      
         private RewardedVideoAd mReward;
         private Button btn;
         
         @Override
         protected void onCreate(Bundle savedInstanceState)
         {
	  super.onCreate(savedInstanceState);
	  setContentView(R.layout.reward_ad);
	  
	  //MobileAds.initialize(this,"ca-app-pub-6514829985639808/7412704160");	  
	  mReward = MobileAds.getRewardedVideoAdInstance(this);
	  mReward.loadAd("Rewarded_Ad_Unit_Id",new AdRequest.Builder().build());
	  //loadVideoAd();
	  
	  btn = findViewById(R.id.btn);
	  btn.setOnClickListener(new View.OnClickListener(){
      
			@Override
			public void onClick(View p1)
			{
			   if(mReward.isLoaded()){
				  mReward.show();
			   }
			}
			
		 
	  });
	  
         }
      
      }
   ```
   
   </details>

<a href="#index">⬆ Back to Top</a>
