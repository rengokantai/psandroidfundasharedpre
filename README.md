#### psandroidfundasharedpre
######2
SharedPreferences: store primitive data in kv pair  
internal storage: store private data on device memory  
exter: store public data on the shared external storage  
sqlite databases: store structured data in a private db  
######6 Accessbility of sharedpreferences
only use
```
MODE_PRIVATE
```
######8 How to create
Activity level: Use if you want a seperate SharedPrederences file for Activity  
```
getPreferences(mode)
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
pkg.file_name.xml
```
######9 SharedPreferences at Act lvl
```
SharedPreferences s = getPrederences(Context.MODE_PRIVATE);
SharedPreferences.Editor e = s.edit();
e.putString("name",editText1.getText().toString());
e.putInt("id":123);
e.apply();//async //or e.commit();//sync
```
get
```
SharedPreferences s = getPrederences(Context.MODE_PRIVATE);
String a = s.getString("name","NA");
```
check generated xml files:  
Android device monitor: from right 3rd button.->DDMS->file explorer  
data->data->com.name->shared_prefs -> then right top corner pull a file from the device

######10 App lvl
open 2nd Activity
```
Intent i = new Intent(this, Second.class);
startActivity(intent);
```
set SharedPreferences file name, need to add package name
```
SharedPreferences s = getSharedPrederences(getPackageName()+".ke", Context.MODE_PRIVATE);
```
######12 Toggle
```
switch.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener(){
  @Override
  public void onCheckedChanged(CompoundButton v,boolean isChecked){
    editor.putBoolean("k",isChecked);
    pageLayout.setBackgroundColor(isChecked? Color.GREEN:Color.RED);
  }
});
boolean isChecked = pref.getBoolean("k",false);
switch.setChecked(isChecked)
```
######13 clear and remove
clear
```
editor.clear();
editor.apply();
```
remove
```
editor.remove("k");
editor.apply();
```


######16 set GSON proj
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
######17 GSON to store a simple
add dependencies GSON. in build.gradle
```
compile 'com.google.code.gson:gson:2.7'
```
serialization/save  
```
Employee e = new Employee();
e.setName("ke");
SharedPreferences a = getPreferences(Context.MODE_PRIVATE);
SharedPreferences.Editor ed = s.edit();

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

######19 Saving and retriving the generic type
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
