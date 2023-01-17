<h1 align="center">
Android Data Storage
</h1>

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

## SQLite
* It is a relational DataBase
* It is an open source DataBase that stores data to a text file on a device
* Android comes in with built in SQLite DataBase implementation
* SQLite is a local DataBase

* **Important Things!**
	* SQLiteOpenHelper `class`
	* super(parameter)


