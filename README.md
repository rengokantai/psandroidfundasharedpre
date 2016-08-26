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
