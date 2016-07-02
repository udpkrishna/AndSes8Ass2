# AndSes8Ass2

MainActivity.java
package me.rk.andses8ass2;

import android.content.Context;
import android.content.SharedPreferences;
import android.support.v4.content.ContextCompat;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private TextView passwordKey;
    private EditText passwordValue;
    private CheckBox screenlockCheckBox;
    private Button saveButton;
    private Button showButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        passwordKey=(TextView)findViewById(R.id.password);
        passwordValue=(EditText)findViewById(R.id.passwordEditText);
        screenlockCheckBox=(CheckBox)findViewById(R.id.screenlock);
//        final boolean lock=screenlockCheckBox.isChecked();
        saveButton=(Button)findViewById(R.id.save);
        saveButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String key1=screenlockCheckBox.getText().toString();
                boolean lock=screenlockCheckBox.isChecked();
                String key=passwordKey.getText().toString();
                String value=passwordValue.getText().toString();
                        if(value.length()==0){
                            Toast.makeText(MainActivity.this, "Password cannot be empty", Toast.LENGTH_SHORT).show();
                            return;
                        }
                saveSharedPref(key, value, key1, lock, MainActivity.this);
                }
        });

        showButton=(Button)findViewById(R.id.show);
        showButton.setOnClickListener(new View.OnClickListener() {
            String key=passwordKey.getText().toString();
            String key1=screenlockCheckBox.getText().toString();
            @Override
            public void onClick(View v) {
                String value=showValueFromSharedPref(key,MainActivity.this);
                passwordValue.setText(value);
                Boolean value1=showValue1FromSharedPref(key1, MainActivity.this);
                screenlockCheckBox.setChecked(value1);
            }
        });
    }

    private void saveSharedPref(String key, String value, String key1, Boolean lock, Context context){
        SharedPreferences sharedPreferences=context.getSharedPreferences("RK_PREF",Context.MODE_PRIVATE);
        SharedPreferences.Editor editor=sharedPreferences.edit();
        editor.putString(key, value);
        editor.putBoolean(key1,lock);
        editor.commit();
    }

    private String showValueFromSharedPref(String key, Context context){
        SharedPreferences sharedPreferences=context.getSharedPreferences("RK_PREF", Context.MODE_PRIVATE);
        String value=sharedPreferences.getString(key, "No Value");
        return value;
    }

    private Boolean showValue1FromSharedPref(String key1, Context context){
        SharedPreferences sharedPreferences=context.getSharedPreferences("RK_PREF", Context.MODE_PRIVATE);
        boolean value1=sharedPreferences.getBoolean(key1, false);
        return value1;
    }
}


activity.main.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="me.rk.andses8ass2.MainActivity"
    android:background="@color/ripple_material_light">

    <TextView
        android:id="@+id/settings"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="SETTINGS"
        android:textColor="@android:color/black"
        android:padding="15dp"/>

    <TextView
        android:id="@+id/password"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Password"
        android:layout_below="@id/settings"
        android:textSize="23dp"
        android:textColor="@android:color/black"
        android:padding="5dp"/>

    <EditText
        android:id="@+id/passwordEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/password"
        android:hint="Set Your Password"/>

    <TextView
        android:id="@+id/securitysettings"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="SECURITY SETTINGS"
        android:layout_below="@id/passwordEditText"
        android:textColor="@android:color/black"
        android:padding="15dp"/>

    <CheckBox
        android:id="@+id/screenlock"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Screen Lock"
        android:layout_below="@id/securitysettings"
        android:textSize="23dp"
        android:textColor="@android:color/black"
        android:padding="5dp"/>

    <TextView
        android:id="@+id/lockthescreenwithpassword"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/screenlock"
        android:hint="Lock The Screen With Password"
        android:padding="5dp"/>

    <TextView
        android:id="@+id/remainderforupdation"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Remainder for Updation"
        android:layout_below="@id/lockthescreenwithpassword"
        android:textSize="23dp"
        android:textColor="@android:color/black"
        android:padding="5dp"/>

    <TextView
        android:id="@+id/setupdateremainderfrequency"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/remainderforupdation"
        android:hint="Set Update Reminder Frequency"
        android:padding="5dp"/>

    <Button
        android:id="@+id/save"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_below="@id/setupdateremainderfrequency"
        android:text="SAVE"
        android:textColor="@android:color/black"/>

    <Button
        android:id="@+id/show"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_below="@id/save"
        android:text="SHOW"
        android:textColor="@android:color/black"/>

</RelativeLayout>

