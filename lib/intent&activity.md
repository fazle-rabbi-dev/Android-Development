<h1 align="center">Intent & Activity</h1>

* [Activity](#)
* [Activity Lifecycle](#)
* [Intent](#)
* [Activity For Result](#)

## Activity
* Every screen is an Activity


## Activity Lifecycle
<div align="center">
   <img width="80%" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTWdJX3dDnx8lNzr0rcqrdS9ale3OsRxaVTAA&usqp=CAU" alt="Activity Lifecycle" />
</div>

## Intent
```java
Intent intent = new Intent(getApplicationContext(),NewActivity.class);
// sending data
intent.putExtra("key","Value");
startActivity(intent);

// receive data from intent
// NewActivity.java

Bundle bundle = getIntent().getExtras();
String value = bundle.getString("key");

// before setContentView get data from intent
setContentView(R.layout.activity_main);


```

## Activity For Result
```java
// MainActivity.java
public class MainActivity extends Activity { 
     
    private Button btn;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        setContentView(R.layout.activity_main);
        
        btn = findViewById(R.id.aboutId);
        btn.setOnClickListener(new View.OnClickListener(){

                @Override
                public void onClick(View p1) {
                    Intent intent = new Intent(getApplicationContext(),AboutActivity.class);
                    startActivityForResult(intent,1);
                }                           
        });
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {   
        super.onActivityResult(requestCode, resultCode, data);
        if(requestCode == 1){
          String name = data.getStringExtra("name");
          Toast.makeText(this,"Hello "+name,Toast.LENGTH_SHORT).show();
        }
    }
     
} 


// AboutActivity.java
public class AboutActivity extends Activity {
    private Button btn;
    private EditText nameField;
    private TextView text;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.about);
        
        btn = findViewById(R.id.btn);
        nameField = findViewById(R.id.name);
        text = findViewById(R.id.text);
        
        btn.setOnClickListener(new View.OnClickListener(){

                @Override
                public void onClick(View p1) {
                    String value = nameField.getText().toString();
                    text.setText("Name: "+value);
                    
                    Intent intent = new Intent(getApplicationContext(),MainActivity.class);
                    intent.putExtra("name",value);
                    setResult(1,intent);
                    finish();
                }
                
            
        });
    }
    
}
```
