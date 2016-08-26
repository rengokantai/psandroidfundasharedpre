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
