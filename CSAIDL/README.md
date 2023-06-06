# Ex.No:2 Create a simple application client and server service using AIDL interface in android studio.


## AIM:

To create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as CSAIDL and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display message give in MainActivity file(client/server).

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the client/server services using AIDL”.
Developed by: G venkata Pavan Kumar
Registeration Number : 212221240013
*/
```
### MainActivity.java:
~~~
package com.example.myaidl;

import androidx.appcompat.app.AppCompatActivity;

import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    EditText editfirstNumber, editsecondNumber;
    Button btnMultiply;
    TextView txtMultiplyRes;

    MultiplyInterface myInteface;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editfirstNumber = (EditText) findViewById(R.id.editfirstNumber);
        editsecondNumber = (EditText) findViewById(R.id.editsecondNumber);
        btnMultiply = (Button) findViewById(R.id.btnMultiply);
        txtMultiplyRes=(TextView) findViewById(R.id.txtMultiplyRes);

        btnMultiply.setOnClickListener(MainActivity.this);
        Intent Mulservice = new Intent(MainActivity.this,Mservice.class);
        bindService(Mulservice, myServiceConnection, Context.BIND_AUTO_CREATE);


    }
    ServiceConnection myServiceConnection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
                myInteface = MultiplyInterface.Stub.asInterface(iBinder);

        }

        @Override
        public void onServiceDisconnected(ComponentName componentName) {
        }
    };
    @Override
    public void onClick(View view) {
        int firstNumber = Integer.parseInt(editfirstNumber.getText().toString());
        int secondNumber = Integer.parseInt(editsecondNumber.getText().toString());
        try{
            int result = myInteface.multiplaytwovaluestogether(firstNumber,secondNumber);
            txtMultiplyRes.setText(result+" ");
        }catch(RemoteException e){
            e.printStackTrace();
        }
    }
}
~~~
### MService.java:
~~~
package com.example.myaidl;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;
import android.os.RemoteException;

public class Mservice extends Service {
    public Mservice() {
    }

    @Override
    public IBinder onBind(Intent intent) {
        return myBinder;

    }
    MultiplyInterface.Stub myBinder = new MultiplyInterface.Stub() {
        @Override
        public int multiplaytwovaluestogether(int firstNumber, int secondNumber) throws RemoteException {
            return firstNumber * secondNumber;
        }
    };
}
~~~
### MultiplyInterface.aidl:
~~~
// MultiplyInterface.aidl
package com.example.myaidl;

// Declare any non-default types here with import statements

interface MultiplyInterface {
    int multiplaytwovaluestogether(int firstNumber, int secondNumber);

}
~~~
### activity_main.xml:
~~~
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="16dp"
    android:paddingLeft="16dp"
    android:paddingRight="16dp"
    android:paddingTop="16dp"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/editfirstNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="number" />

    <EditText
        android:id="@+id/editsecondNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="number" />

    <Button
        android:id="@+id/btnMultiply"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Multiply" />

    <TextView
        android:id="@+id/txtMultiplyRes"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Result" />
</LinearLayout>


~~~


## OUTPUT
![image](https://github.com/Pavan-Gv/Advance-Android-Odd-/assets/94827772/60845013-210d-462f-95ae-7bd74fa7428c)
![image](https://github.com/Pavan-Gv/Advance-Android-Odd-/assets/94827772/61434a86-e6f7-4488-944d-2489fef0e5c5)




## RESULT
Thus a Simple Android Application to create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio is developed and executed successfully.
