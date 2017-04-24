# psandroidfundasharedpre
## 2. Introduction
### 1 Introduction to Android Storage Options
SharedPreferences
- store primitive data in key-value pair  
internal storage  
- store private data on device memory  
external storage  
- store public data on the shared external storage  
sqlite databases  
- store structured data in a private db  
Network Connection  
- Store data on the web with your own network server  

## 3. Saving and Retriving Data from SharedPreferences
### 1 Introduction
Store only promitive ata type  
- String 
- int 
- float 
- boolean
### 2 Accessbility of Sharedpreferences
Now, the SharedPreferences file can have the private access within the application.  
That is, no other application can have access to your ShaedPreferences file present within your application.  



only use
```
MODE_PRIVATE
```
File can be accessible to other apps (deprecated)
```
MODE_WORLD_READABLE  //Deprecated in API17
```

### 3 Initial Project Setup
Empty Activity
```
loadAccountData
clearAccountData
removeProfessionKey
```

### 4 How to Create and Access the SharedPreference
Activity level
- Use if you want a seperate SharedPrederences file for Activity  
- If you want to keep the SharedPreferences file private to your activity, then you can use this activity level SharedPreferences file  
Application Level  
- If you want multiple Sharedpreferences files for your app identified by unique name  

```
getPreferences()
```
filename convention:
```
Activity_name.xml //or
MainActivity.xml
```
Application level: If want multiple sharedpreferences files for app identified by unique name
```
getSharedPreferences(String name,int mode)
```
filename convention:
```
<package>file_name.xml "com.example.myapp.my_preference_file.xml"
```
### 5 SharedPreferences at Activity Level
```
SharedPreferences s = getPreferences(Context.MODE_PRIVATE);
SharedPreferences.Editor e = s.edit();
e.putString("name",editText1.getText().toString());
e.putInt("id":123);
e.apply();//async //or e.commit();//sync
```
get
```
SharedPreferences s = getPreferences(Context.MODE_PRIVATE);
String a = s.getString("name","NA");
```
check generated xml files:  
Android device monitor: from right 3rd button.->DDMS->file explorer  
data->data->com.name->shared_prefs -> then right top corner pull a file from the device  

#### 11:42
Unless you uninstall your app, the file is still in your phone

### 6 SharedPreferences at Application Level
open 2nd Activity
```
Intent i = new Intent(this, SecondActivity.class);
startActivity(intent);
```
set SharedPreferences file name, need to add package name
```
SharedPreferences s = getSharedPrederences(getPackageName()+".ke", Context.MODE_PRIVATE);
```
### 8 TogglecApplication Logic Based on Preference Values
```
switch.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener(){
  @Override
  public void onCheckedChanged(CompoundButton buttonView,boolean isChecked){
    editor.putBoolean("k",isChecked);
    pageLayout.setBackgroundColor(isChecked? Color.GREEN:Color.RED);
  }
});
```
```
boolean isChecked = pref.getBoolean("k",false);
switch.setChecked(isChecked)
```
### 9 Perform Clear and Remove Operation
clear
```
editor.clear(); //clears all the key-value pairs in SharedPreferences
editor.apply();
```
remove
```
editor.remove("k");
editor.apply();
```

## 4. Using GSON to Save and etrive Non-primitive Data Type
### 2 Initial Project Setup
```
purblic class Foo<T>{
  private T object;
  public T getObject(){
    return object;
  }
  pubilc void setObject (T Object){
    this.object = Object;
  }
}

public class Employee{
  private String name;
}
```
### 3 Using GSON to Store a Simple Class Object in SharedPreferences
add dependencies GSON. in build.gradle
```
compile 'com.google.code.gson:gson:2.7'
```
serialization/save  
```
Employee e = new Employee();
e.setName("ke");
e.setRoles(Arrays.asList("Developer","Admin");
SharedPreferences sp = getPreferences(Context.MODE_PRIVATE);
SharedPreferences.Editor ed = sp.edit();

Gson g = new Gson();
String s = g.toJson(e,Employee.class);        //note this is string type
Log.i(TAG,s);
ed.putString("k",s);
ed.apply();
```

deserialization/load
```
SharedPreferences a = getPreferences(Context.MODE_PRIVATE);
String s = sharedPreferences.getString("k","NA");
Log.i(TAG,s);
Gson g = new Gson();
Employee e = gson.fromJson(s, Employee.class);
```

### 5 Saving and Retriving the Generic Type Data from SahredPreferences
```
public void saveGeneric(View view){
  Employee e = getEployee();
  Foo<Employee> f = new Foo<>();
  f.setObject(e);
  
  SharedPreferences a = getPreferences(Context.MODE_PRIVATE);
SharedPreferences.Editor ed = s.edit();

Gson g = new Gson();
Type type = new TypeToken<Foo<Employee>>(){}.getType();          //very important
String s = g.toJson(f,type);        //note this is string type
Log.i(TAG,s);
ed.putString("k",s);
ed.apply();
}
```
