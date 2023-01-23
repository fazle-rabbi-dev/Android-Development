<h1 align="center">Api Calling Using HTTTP Volley Library</h1>


* ### Dependency
	```gradle
	implementation 'com.android.volley:volley:1.1.1'
	```

<p id="index"></p>

* ### Fix Twice Request
	```java
	jsonObjectRequest.setRetryPolicy(new DefaultRetryPolicy(
		0,
		DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
		DefaultRetryPolicy.DEFAULT_BACKOFF_MULT
	));
	```
* [Json Array Get Request](#JsonArrayGetRequest)
* [Json Array Get Request And Display Data In RecyclerView](#jsonArrayRequest&display)
* [Json Object Get Requet](#JsonObjectGetRequest)
* [Json String Get Requet](#JsonStringGetRequest)
* [Json Object Post Requet](#JsonObjectPostRequest)

<p id="JsonArrayGetRequest"></p>

## Json Array Get Request
```java
public void getData(){
      
      JsonArrayRequest jsonArrayRequest = new JsonArrayRequest(
         Request.Method.GET,
         URL,
         null,
         new Response.Listener<JSONArray>() {
            @Override
            public void onResponse(JSONArray response) {
               // Handle the JSONArray response here
            }
         },
         new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
               // Handle the error here
            }
         });

        // Add the request to the RequestQueue
        RequestQueue queue = Volley.newRequestQueue(getApplicationContext());
        queue.add(jsonArrayRequest);
}
```

[Back To Top](#index)

<p id="jsonArrayRequest&display"></p>

## Json Array Get Request And Display Data In RecyclerView
* **MainActivity.java**

	<details>
	<summary>Expand Code</summary>
	
	```java
	package com.mycompany.application;
	
	import android.os.Bundle;
	import android.support.v7.app.AppCompatActivity;
	import android.support.v7.widget.LinearLayoutManager;
	import android.support.v7.widget.RecyclerView;
	import android.support.v7.widget.Toolbar;
	import android.view.View;
	import android.widget.Toast;
	import com.android.volley.Request;
	import com.android.volley.RequestQueue;
	import com.android.volley.Response;
	import com.android.volley.VolleyError;
	import com.android.volley.toolbox.JsonArrayRequest;
	import com.android.volley.toolbox.Volley;
	import org.json.JSONArray;
	import java.util.ArrayList;
	import org.json.JSONObject;
	import org.json.JSONException;
	import java.util.Map;
	import java.util.HashMap;
	import android.widget.ProgressBar;
	
	public class MainActivity extends AppCompatActivity {
	   private RecyclerView recyclerView; 
	   private String URL = "https://jsonplaceholder.typicode.com/posts";
	   private ArrayList<ParseObject> allData;
	   private ProgressBar loader;
	   
	   @Override
	   protected void onCreate(Bundle savedInstanceState) {
	      super.onCreate(savedInstanceState);
	      setContentView(R.layout.activity_main);
	
	      Toolbar toolbar=(Toolbar)findViewById(R.id.toolbar);
	      loader = findViewById(R.id.loader);
	      setSupportActionBar(toolbar);
	
	      recyclerView = findViewById(R.id.recyclerView);
	      
	      
	      
	      // initialize arraylist
	      allData = new ArrayList<ParseObject>();
	      getData();
	      
	      
	            
	      MyAdapter adapter = new MyAdapter(getApplicationContext(),allData);
	      recyclerView.setAdapter(adapter);
	   recyclerView.setLayoutManager(new LinearLayoutManager(getApplicationContext()));
	
	   adapter.setOnItemClickListener(new MyAdapter.ClickListener(){
	
	      @Override
	         public void onItemClick(int position, View view) {
	         Toast.makeText(getApplicationContext(),allData.get(position).getTitle().toString(),Toast.LENGTH_SHORT).show();
	         }
	
	            });
	            
	
	   }
	   
	   public void getData(){
	      
	      JsonArrayRequest jsonArrayRequest = new JsonArrayRequest(
	         Request.Method.GET,
	         URL,
	         null,
	         new Response.Listener<JSONArray>() {
	            @Override
	            public void onResponse(JSONArray response) {
	               // Handle the JSONArray response here
	               Toast.makeText(getApplicationContext(),"Data Fetched",Toast.LENGTH_SHORT).show();
	               loader.setVisibility(View.GONE);
	               for(int i=0;i<response.length();i++){
	                  try {
	                     JSONObject obj = response.getJSONObject(i);
	                     ParseObject parsed_object = new ParseObject();
	                     parsed_object.setTitle(obj.getString("title").toString());
	                     parsed_object.setBody(obj.getString("body").toString());
	                     allData.add(parsed_object);
	                     
	                  } catch (JSONException e) {
	                     Toast.makeText(getApplicationContext(),"Something went wrong ==> inside loop",Toast.LENGTH_SHORT).show();
	                  }
	               }               
	                              
	               
	               
	               
	            }
	         },
	         new Response.ErrorListener() {
	            @Override
	            public void onErrorResponse(VolleyError error) {
	               // Handle the error here
	               Toast.makeText(getApplicationContext(),"Something went wrong",Toast.LENGTH_SHORT).show();
	            }
	         });
	
	        // Add the request to the RequestQueue
	        RequestQueue queue = Volley.newRequestQueue(getApplicationContext());
	        queue.add(jsonArrayRequest);
	   }
	   
	
	}
	
	```
	[Back To Top](#index)
	
	</details>

* **MyAdapter..java**

	<details>
	<summary>Expand Code</summary>
	
	```java
	package com.mycompany.application;
	import android.support.v7.widget.RecyclerView;
	import android.view.ViewGroup;
	import android.view.View;
	import android.content.Context;
	import android.view.LayoutInflater;
	import android.widget.TextView;
	import java.util.ArrayList;
	import java.util.HashMap;
	
	public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {
	
	   private Context context;
	   //private String[] title;
	   //private String[] body;
	   private ArrayList<ParseObject> allData;
	   private static ClickListener clickListener;
	
	   MyAdapter(Context context,ArrayList<ParseObject> allData){
	      this.context = context;
	      this.allData = allData;
	   }
	
	   @Override
	   public MyViewHolder onCreateViewHolder(ViewGroup viewGroup, int p2) {
	
	      LayoutInflater inflater = LayoutInflater.from(context);
	      View view =inflater.inflate(R.layout.recycler_view_layout,viewGroup,false);
	      return new MyViewHolder(view);
	   }
	
	   @Override
	   public void onBindViewHolder(MyViewHolder myViewHolder, int i) {
	                        
	      myViewHolder.title.setText(allData.get(i).getTitle());
	      myViewHolder.body.setText(allData.get(i).getBody());
	
	      //myViewHolder.countryName.setText("Test");
	      //myViewHolder.countryDetails.setText("ok");
	
	
	   }
	
	   @Override
	   public int getItemCount(){
	      return allData.size();
	   }
	
	
	   class MyViewHolder extends RecyclerView.ViewHolder implements View.OnClickListener {
	
	      TextView title,body;
	
	      public MyViewHolder(View itemView){
	         super(itemView);
	
	         title = itemView.findViewById(R.id.title);
	         body = itemView.findViewById(R.id.body);
	
	         // set listener
	         itemView.setOnClickListener(this);
	      }
	
	      @Override
	      public void onClick(View view) {
	         clickListener.onItemClick(getAdapterPosition(),view);
	      }      
	
	   }
	
	   public interface ClickListener{
	      void onItemClick(int position,View view);
	   }
	
	   public void setOnItemClickListener(ClickListener clickListener){
	      MyAdapter.clickListener = clickListener;
	   }
	
	}			
	```
	[Back To Top](#index)

	</details>

* **ParseObject.java**

	<details>
	<summary>Expand Code</summary>
	
	```java
	package com.mycompany.application;
	
	public class ParseObject {
	    
	    private String title;
	    private String body;
	    
	    public ParseObject(){}
	    
	    
	    public void setTitle(String title){
	       this.title = title;
	    }
	    
	    public void setBody(String body){
	       this.body = body;
	    }
	    
	    public String getTitle(){
	       return title;
	    }
	    
	   public String getBody(){
	      return body;
	   }
	
	   
	    
	}	
	```
	[Back To Top](#index)
	
	</details>


[Back To Top](#index)

<p id="JsonObjectGetRequest"></p>

## Json Object Get Request
```java
// Object Get Request
public void getObject(String url){
   JsonObjectRequest jsonArrayRequest = new JsonObjectRequest(
      Request.Method.GET,
      url,
      null,
      new Response.Listener<JSONObject>() {
         @Override
         public void onResponse(JSONObject response) {
            // Handle the JSONArray response here
            try {
               Toast.makeText(getApplicationContext(), "Response: " + response.getString("title").toString(), Toast.LENGTH_SHORT).show();
            } catch (JSONException e) {
               
            }
         }
      },
      new Response.ErrorListener() {
         @Override
         public void onErrorResponse(VolleyError error) {
            // Handle the error here
         }
      });

   // Add the request to the RequestQueue
   RequestQueue queue = Volley.newRequestQueue(getApplicationContext());
   queue.add(jsonArrayRequest);
}
```

[Back To Top](#index)

<p id="JsonStringGetRequest"></p>

## Json String Get Request
```java
public void getString(){
	StringRequest stringRequest = new StringRequest(Request.Method.POST, "https://example.com",
	    new Response.Listener<String>() {
	        @Override
	        public void onResponse(String response) {
	            // Handle the response
	        }
	    },
	    new Response.ErrorListener() {
	        @Override
	        public void onErrorResponse(VolleyError error) {
	            // Handle the error
	        }
	    }) {
	    @Override
	    public byte[] getBody() {
	        return "request_string".getBytes();
	    }
	};
	
	// Add the request to the RequestQueue.
	queue.add(stringRequest);	
}
```

[Back To Top](#index)

<p id="JsonObjectPostRequest"></p>

## Json Object Post Request
```java
// Method For Post Request
public void postRequest(String name,String age){
   String url = "https://jsonplaceholder.typicode.com/posts";

   // Create a new RequestQueue
   RequestQueue queue = Volley.newRequestQueue(this);

   // Create a new JSONObject to send as the POST body
   JSONObject jsonBody = new JSONObject();
   try {
      jsonBody.put("Name", name);
      jsonBody.put("Age", age);
   } catch (JSONException e) {
      e.printStackTrace();
   }

   // Create a new JsonObjectRequest
   JsonObjectRequest jsonObjectRequest = new JsonObjectRequest(Request.Method.POST, url, jsonBody,
      new Response.Listener<JSONObject>() {
         @Override
         public void onResponse(JSONObject response) {
            // Handle the server response here
            
            try {
               String name = response.getString("Name").toString();
               Toast.makeText(getApplicationContext(), "Ok: "+name, Toast.LENGTH_SHORT).show();
            } catch (JSONException e) {
               Toast.makeText(getApplicationContext(), "error: "+e, Toast.LENGTH_SHORT).show();
            }
            
            
         }
      }, new Response.ErrorListener() {
         @Override
         public void onErrorResponse(VolleyError error) {
            // Handle errors here
            Toast.makeText(getApplicationContext(),"Error",Toast.LENGTH_SHORT).show();
         }
      });

   // Add the request to the RequestQueue
   queue.add(jsonObjectRequest);
}
```

[Back To Top](#index)

