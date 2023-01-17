<h1 align="center">
Android Data Storage
</h1>

<p id="index"></p>

* [Shared Preference](#)
* [File Storage](#)
* [SQLite](#)
* [Firebase](#)

## Shared Preference
```java
// for write data
SharedPreferences sp = getSharedPreferences("NotesData",Context.MODE_PRIVATE);
SharedPreferences.Editor editor = sp.edit();
editor.putString("userName",uName);
editor.putString("userPassword",uPass);
editor.commit();

// for read data
SharedPreferences sp = getSharedPreferences("NotesData",Context.MODE_PRIVATE);
String userName = sp.getString("userName","Data not found");
```

## File Storage
```java
 // Write Data to file storage
      btn.setOnClickListener(new View.OnClickListener(){

            @Override
            public void onClick(View view) {
               String uName = userName.getText().toString();
               String uPass = userPassword.getText().toString();
               
               try {
                  FileOutputStream fos = openFileOutput("notes.txt", Context.MODE_PRIVATE);
                  try {
                     fos.write(uName.getBytes());
                     fos.close();
                     Toast.makeText(getApplicationContext(),"Data saved",Toast.LENGTH_SHORT).show();
                  } catch (IOException e) {
                     e.printStackTrace();
                  }

                  
               } catch (FileNotFoundException e) {
                  e.printStackTrace();
               }

               
            }
            
         
      });
      
      // Read Data from file storage
      btn2.setOnClickListener(new View.OnClickListener(){

            @Override
            public void onClick(View view) {
               
               try {
                  FileInputStream fis = openFileInput("notes.txt");
                  InputStreamReader isr = new InputStreamReader(fis);
                  BufferedReader bfr = new BufferedReader(isr);
                  String line;
                  StringBuffer stringBffer = new StringBuffer();
                  
                  try {
                     while ((line = bfr.readLine()) != null) {
                        stringBffer.append(line+"\n");
                     }
                  } catch (IOException e) {
                     e.printStackTrace();
                  }
                  
                  Toast.makeText(getApplicationContext(),stringBffer,Toast.LENGTH_SHORT).show();

               } catch (FileNotFoundException e) {
                  e.printStackTrace();
               }
                              
            }
            
         
      });
```

<a href="#index">⬆ Back to Top</a>

## SQLite
* It is a relational DataBase
* It is an open source DataBase that stores data to a text file on a device
* Android comes in with built in SQLite DataBase implementation
* SQLite is a local DataBase

* **Important Things!**
	* SQLiteOpenHelper `class`
	* super(parameter)
* ### CRUD Operation:
* **MyDatabaseHelper.java**
	```java
	public class MyDatabaseHelper extends SQLiteOpenHelper {
	
	   private static final String DB_NAME = "StudentDB";
	   private static final String TABLE_NAME = "StudentDetails";
	   private static final int DB_VERSION = 5;
	   private String ID = "_ID";
	   private String NAME = "NAME";
	   private String AGE = "AGE";
	   // New Column
	   private String GENEDER = "GENDER";
	   private String CITY = "CITY";
	   private Context context;
	   // SQL Command   
	   private String CREATE_TABLE = "CREATE TABLE "+TABLE_NAME+"("+ID+" INTEGER PRIMARY KEY AUTOINCREMENT,"+NAME+" VARCHAR(255),"+AGE+" INTEGER, "+GENEDER+" VARCHAR(255) ,"+CITY+" VARCHAR(255) ); ";
	   private String DROP_TABLE = "DROP TABLE IF EXISTS "+TABLE_NAME;
	      
	   public MyDatabaseHelper(Context context){
	      super(context,DB_NAME,null,DB_VERSION);
	      this.context = context;
	   }
	   
	   
	   // For Create Database & Table
	   @Override
	   public void onCreate(SQLiteDatabase SQLite) {
	      try {
	         Toast.makeText(context,"Oncreate Called !",Toast.LENGTH_LONG).show();
	         SQLite.execSQL(CREATE_TABLE);
	      } catch (SQLException e) {
	         Toast.makeText(context,"Error inside onCreate: "+e,Toast.LENGTH_LONG).show();
	      }
	   }
	
	   
	   // For Upadate Table Ex:column
	   @Override
	   public void onUpgrade(SQLiteDatabase SQLite, int p2, int p3) {
	      try {
	         SQLite.execSQL(DROP_TABLE);
	         onCreate(SQLite);
	         Toast.makeText(context, "On Upgrade Called !", Toast.LENGTH_LONG).show();
	      } catch (SQLException e) {
	         Toast.makeText(context,"Error inside upgradr: "+e,Toast.LENGTH_LONG).show();
	      }
	   }
	   
	   
	   // For Add Data Inside Table
	   public long insertData(String name,String age,String gender,String city){
	      SQLiteDatabase sqldb = this.getWritableDatabase();
	      ContentValues cv = new ContentValues();
	      cv.put(NAME,name);
	      cv.put(AGE,age);
	      cv.put(GENEDER,gender);
	      cv.put(CITY,city);
	      long row_id = sqldb.insert(TABLE_NAME,null,cv);
	      
	      return row_id;
	   }
	   
	   
	   // For Read/Display Data From Table
	   public Cursor displayData(){
	      SQLiteDatabase sqldb = this.getWritableDatabase();
	      Cursor cursor =  sqldb.rawQuery("SELECT * FROM "+TABLE_NAME,null);
	      return cursor;      
	   }
	   
	   // For Update Data
	   public Boolean updateData(String id,String name,String age,String gender,String city){
	      SQLiteDatabase sqldb = this.getWritableDatabase();
	      ContentValues cv = new ContentValues();
	      cv.put(ID,id);
	      cv.put(NAME,name);
	      cv.put(AGE,age);
	      cv.put(GENEDER,gender);
	      cv.put(CITY,city);
	      sqldb.update(TABLE_NAME,cv,ID+" = ?",new String[] { id });
	      return true;
	   }
	   
	   // For Delete Data
	   public int deleteData(String id){
	      SQLiteDatabase sqldb = this.getWritableDatabase();
	      return sqldb.delete(TABLE_NAME,ID+" = ?",new String[] { id });
	   }
	            
	}	
	```

<a href="#index">⬆ Back to Top</a>

* **MainActivity.java**
	```java
	package com.mycompany.application;
	 
	import android.app.Activity;
	import android.os.Bundle;
	import android.view.View;
	import android.widget.Button;
	import android.widget.EditText;
	import android.widget.Toast;
	import android.view.View.OnClickListener;
	import android.database.Cursor;
	import android.app.AlertDialog;
	import android.os.Build;
	import android.widget.Magnifier.Builder;
	
	public class MainActivity extends Activity { 
	    
	   private MyDatabaseHelper mydbhelper;
	   private Button saveBtn,displayBtn,updateBtn,deleteBtn;
	   private EditText name,age,gender,city,id;
	   
	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	         
	         name = findViewById(R.id.name);
	         age = findViewById(R.id.age);
	         gender = findViewById(R.id.gender);
	         city = findViewById(R.id.city);
	         id = findViewById(R.id.id);
	         saveBtn = findViewById(R.id.btn);
	         displayBtn = findViewById(R.id.displayBtn);
	         updateBtn = findViewById(R.id.updateBtn);
	         deleteBtn = findViewById(R.id.deleteBtn);
	         mydbhelper = new MyDatabaseHelper(getApplicationContext());
	       
	         
	       // Create Data
	       saveBtn.setOnClickListener(new View.OnClickListener(){
	
	             @Override
	             public void onClick(View p1) {
	                String NAME = name.getText().toString();
	                String AGE = age.getText().toString();
	                String GENDER = gender.getText().toString();
	                String CITY = city.getText().toString();                                
	                
	                //SQLiteDatabase sqlite_db = mydbhelper.getWritableDatabase();
	                long row_id = mydbhelper.insertData(NAME,AGE,GENDER,CITY);
	                Toast.makeText(getApplicationContext(),"Data inserted successfully: "+ row_id,Toast.LENGTH_SHORT).show();
	                
	             }
	                         
	         });
	         
	       
	       // Read Data
	       displayBtn.setOnClickListener(new View.OnClickListener(){
	
	             @Override
	             public void onClick(View view) {
	                Cursor cursor = mydbhelper.displayData();
	                if(cursor.getCount() != 0){
	                   
	                   StringBuffer stringBuffer = new StringBuffer();
	                   while(cursor.moveToNext()){
	                      stringBuffer.append("ID: "+cursor.getString(0)+"\n");
	                      stringBuffer.append("NAME: "+cursor.getString(1)+"\n");
	                      stringBuffer.append("AGE: "+cursor.getString(2)+"\n");
	                      stringBuffer.append("GENDER: "+cursor.getString(3)+"\n");
	                      stringBuffer.append("CITY: "+cursor.getString(4)+"\n\n\n");
	                   }
	                   
	                   // Show Data In Alert
	                   showData("All Data",stringBuffer.toString());
	                   
	                }
	                // If not found table
	                else{
	                   Toast.makeText(getApplicationContext(),"Table not found",Toast.LENGTH_SHORT).show();
	                }
	             }
	                         
	         });
	         
	         
	       // Update Data
	       updateBtn.setOnClickListener(new View.OnClickListener(){
	    
	             @Override
	             public void onClick(View p1) {
	                String NAME = name.getText().toString();
	                String AGE = age.getText().toString();
	                String GENDER = gender.getText().toString();
	                String CITY = city.getText().toString();                                
	                String ID = id.getText().toString();                                
	                
	                Boolean isUpdated = mydbhelper.updateData(ID,NAME,AGE,GENDER,CITY);
	                if(isUpdated == true){
	                   Toast.makeText(getApplicationContext(),"Updated Successfull",Toast.LENGTH_SHORT).show();
	                }
	                else{
	                   Toast.makeText(getApplicationContext(),"Updated Unsuccessfull",Toast.LENGTH_SHORT).show();
	                }
	             }
	                         
	         });
	         
	         
	         // Delete Data
	       deleteBtn.setOnClickListener(new View.OnClickListener(){
	
	             @Override
	             public void onClick(View p1) {
	                String ID = id.getText().toString();                                
	                int value = mydbhelper.deleteData(ID);
	                if(value != 0){
	                   Toast.makeText(getApplicationContext(),"Deleted Successfull",Toast.LENGTH_SHORT).show();
	                }
	                else{
	                   Toast.makeText(getApplicationContext(),"Deleted Unsuccessfull",Toast.LENGTH_SHORT).show();
	                }
	             }
	                         
	         });
	         
	                           
	    }
	    
	    public void showData(String title,String data){
	       AlertDialog.Builder adb = new AlertDialog.Builder(this);
	       adb.setTitle(title);
	       adb.setMessage(data);
	       adb.show();
	    }
		
	} 
	
	```

<a href="#index">⬆ Back to Top</a>
