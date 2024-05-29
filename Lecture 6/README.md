## We install the APK to the emulator by typing the below command.
 
 ```
adb install diva-beta.apk
```

![image](https://github.com/ananthan05/Android-Security/assets/140697378/77d9b93a-8cd7-4ad7-bea5-9a2364138370)

 ## 1. Insecure Logging
 
 We type adb logcat in the terminal window.
 ```
adb logcat | grep-i "credit card"
```
 We click on the Insecure Logging button.
 We type a number in the EditText field and click on the Check Out button.
 We observe that An error occurred toast message is shown, and that the logcat has logged the input that
 was entered.
 
![image](https://github.com/ananthan05/Android-Security/assets/140697378/bf64d4c3-5afa-4835-87c6-d9ed2ad001ca)

We open JADX and open the diva-beta.apk file.
We observe the decompiled source code and open the LogActivity in the JADX

![image](https://github.com/ananthan05/Android-Security/assets/140697378/7f2114a7-0a97-40cc-9425-627b173ad1ca)

## 2. Hardcoding Issues- Part 1

 We observe the decompiled source code and open the HardcodeActivity in the JADX.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/7426f000-21b9-4c55-80a9-399d20ca1c3f)

We type the hardcoded vendor key in the EditText field.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/470c9331-dc7a-4468-94e7-9224211d9459)

## 3. Insecure Data Storage- Part 1
 
 We explore the application by entering username and password in the EditText field

 ![Screenshot 2024-05-29 101003](https://github.com/ananthan05/Android-Security/assets/140697378/f1d2d0a9-a0a3-4cbb-8363-0c5178c74f34)

We use adb shell to explore the file system used by the application

![image](https://github.com/ananthan05/Android-Security/assets/140697378/06af5aac-82ab-46af-9255-c71ea4f5097e)

 Inside the `/data/data/jakhar.aseem.diva` directory, we notice the databases and shared_prefs directory.

 We type cat shared_prefs/jakhar.aseem.diva_preferences.xml to see the username and password thatwere saved by the application

![image](https://github.com/ananthan05/Android-Security/assets/140697378/5cb0abc0-142c-401e-8334-b514b98540ba)

We observe the decompiled source code and open the InsecureDataStorage1Activity in the JADX.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/cd498aab-5660-49c2-98cd-a1c87ee752a3)

## 4. Insecure Data Storage- Part 2

 We explore the application by entering username and password in the EditText field.

 ![image](https://github.com/ananthan05/Android-Security/assets/140697378/479fd969-d5ff-493c-8eb1-8ef6f0331924)

We use adb shell to explore the file system used by the application.

 Inside the `/data/data/jakhar.aseem.diva directory`, we notice the databases and shared_prefs directory.
 
 We observe that there is a new file inside the databases directory

 ![image](https://github.com/ananthan05/Android-Security/assets/140697378/7a474f53-34b2-45a0-90a6-39c52f9c5dc8)

 We open the `ids2` database using the `sqlite3 program`, and enter `select * from myuser`; to view the
 saved username and password

 ![image](https://github.com/ananthan05/Android-Security/assets/140697378/4995091a-c8d9-4700-86e2-07be9e4c4a38)

 We observe the decompiled source code and open the InsecureDataStorage2Activity in the JADX

 ![image](https://github.com/ananthan05/Android-Security/assets/140697378/cee3a7ac-f1a6-4446-b63b-e21130364c34)


## 5. Insecure Data Storage- Part 3
 
We explore the application by entering username and password in the EditText field.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/84a878a0-f829-4e13-9d48-035045226fac)

We use adb shell to explore the file system used by the application.

 Inside the `/data/data/jakhar.aseem.diva directory`, we observe that there is a new file with the name
 `uinfo-1455578291tmp`. We display the contents of the file using the `cat uinfo-1455578291tmp` command.

 ![image](https://github.com/ananthan05/Android-Security/assets/140697378/7146f790-2b83-48e3-bd17-e2d8ae9887be)

username and passward-

 ![image](https://github.com/ananthan05/Android-Security/assets/140697378/b53e4505-1ed5-408e-8060-6beda3e6f2cc)

  We observe the decompiled source code and open the InsecureDataStorage3Activity in the JADX

![image](https://github.com/ananthan05/Android-Security/assets/140697378/29637c08-ffdb-4401-8cfb-fcaa37fd293f)


 ## 6. Insecure Data Storage- Part 4
 
 We explore the application by entering username and password in the EditText field

![image](https://github.com/ananthan05/Android-Security/assets/140697378/1c519fd5-1158-4b73-80e2-6a00c47aecb7)

We observe the decompiled source code and open the InsecureDataStorage4Activity in the JADX

![image](https://github.com/ananthan05/Android-Security/assets/140697378/893cde21-c093-42fc-afaa-e17201878115)

As it is located in external storage, In the adb shell, we navigate to cd /sdcard and type the commands: ls -a and cat .uinfo.txt to view the contents of the file.


![image](https://github.com/ananthan05/Android-Security/assets/140697378/4b3ce713-a74d-4f37-9f92-bf273fad8c0f)
