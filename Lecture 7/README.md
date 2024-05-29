 ## 7. Input Validation Issues- Part 1
    
 We explore the application by entering values in the search EditText field

![image](https://github.com/ananthan05/Android-Security/assets/140697378/391a58a9-1cc1-4f6a-ac39-c8ceeec777ce)

We observe the decompiled source code in the JADX.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/44420471-327e-4f2b-baed-37facac51c3d)

We understand that for this Task an activity called SQLInjectionActivity is used.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/0c7d1dda-31cf-4df8-83d2-8ce079525e6d)

We enter `1' OR 1=1--` so that the above SQL query becomes
```sql
SELECT * FROM sqliuser WHERE user ='1' OR 1=1--' 
```
The WHERE clause condition gets evaluated to FALSE or TRUE which is equivalent to TRUE, hence all the records in the database are displayed in the Toast message.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/2e625f47-8371-4359-a686-f250e39cd722)


## 8. Input Validation Issues- Part 2
 
 We explore the application by entering values in the URL EditText field.

 ![image](https://github.com/ananthan05/Android-Security/assets/140697378/d16ec968-4e3b-45c9-b55f-1079f4fec4fb)

We enter a sensitive path like `file:///data/data/jakhar.aseem.diva/jakhar.aseem.diva_preferences.xml`

which only the application has access to and normal user of the device does not have access to. We observe
that the file contents are displayed in the WebView.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/95181e68-a3e1-48d3-908e-6f28ccfabd3a)

We observe the decompiled source code and open the InputValidation2URISchemeActivity in the JADX.

We observe that the user input value in the EditText field is used directly to load in the WebView without any sanitization or validation.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/792a3123-c688-488e-b98f-3c1231fe253b)
