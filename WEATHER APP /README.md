## ANANTHANARAYANAN S
## CB.SC.P2CYS23007

## Weather app 

### Androidmanifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
<uses-permission android:name="android.permission.INTERNET"/>
    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Weather_App"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

![image](https://github.com/ananthan05/Android-Security/assets/140697378/5cb11222-8eae-4c6f-af81-0aa57023ac73)


### MainActivity.java

```java
package com.example.weather_app;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.os.*;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import org.json.JSONObject;
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.concurrent.ExecutionException;

public class MainActivity extends AppCompatActivity {
    TextView cityName;
    Button search;
    TextView show;
    String url;


    class getWeather extends AsyncTask<String, Void, String>{
        @Override
        protected String doInBackground(String... urls){
            StringBuilder result = new StringBuilder();
            try{
                URL url= new URL(urls[0]);
                HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
                urlConnection.connect();

                InputStream inputStream = urlConnection.getInputStream();
                BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));

                String line="";
                while((line = reader.readLine()) != null){
                    result.append(line).append("\n");
                }
                return result.toString();
            }catch(Exception e){
                e.printStackTrace();
                return null;
            }
        }
        @Override
        protected void onPostExecute(String result){
            super.onPostExecute(result);
            try{
                JSONObject jsonObject = new JSONObject(result);
                JSONObject main = jsonObject.getJSONObject("main");

                double tempKelvin = main.getDouble("temp");
                double feelsLikeKelvin = main.getDouble("feels_like");
                double tempMaxKelvin = main.getDouble("temp_max");
                double tempMinKelvin = main.getDouble("temp_min");
                int pressure = main.getInt("pressure");
                int humidity = main.getInt("humidity");

                double tempCelsius = tempKelvin-273.15;
                double feelsLikeCelsius = feelsLikeKelvin-273.15;
                double tempMaxCelsius = tempMaxKelvin-273.15;
                double tempMinCelsius = tempMinKelvin-273.15;

                String weatherInfo = "Temperature : " + String.format("%.2f", tempCelsius) + " °C\n" +
                        "Feels Like : " + String.format("%.2f", feelsLikeCelsius) + " °C\n" +
                        "Temperature Max : " + String.format("%.2f", tempMaxCelsius) + " °C\n" +
                        "Temperature Min : " + String.format("%.2f", tempMinCelsius) + " °C\n" +
                        "Pressure : " + pressure + " hPa\n" +
                        "Humidity : " + humidity + " %";

                show.setText(weatherInfo);
            }catch(Exception e){
                e.printStackTrace();
            }
        }
    }
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        cityName = findViewById(R.id.cityName);
        search = findViewById(R.id.search);
        show = findViewById(R.id.weather);

        final String[] temp={""};

        search.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View v){
                Toast.makeText(MainActivity.this, "Button Clicked! ", Toast.LENGTH_SHORT).show();
                String city = cityName.getText().toString();
                try{
                    if(city!=null){
                        url = "https://api.openw" +
                                "eathermap.org/data/2.5/weather?q=" + city + "&appid=deb66bf8b78783ede5efaa14cd8dad73";
                    }else{
                        Toast.makeText(MainActivity.this, "Enter City", Toast.LENGTH_SHORT).show();
                    }
                    getWeather task= new getWeather();
                    temp[0] = task.execute(url).get();
                }catch(ExecutionException e){
                    e.printStackTrace();
                }catch(InterruptedException e){
                    e.printStackTrace();
                }
                if(temp[0] == null){
                    show.setText("Cannot able to find Weather");
                }

            }
        });

    }
}

```

![image](https://github.com/ananthan05/Android-Security/assets/140697378/2d1f1a1c-4f4f-47eb-8dba-3d1ba59d803e)

## OUTPUT

we should give the input some palce name i have given as `ettimadai `

my app output.

![image](https://github.com/ananthan05/Android-Security/assets/140697378/4af76ae6-f9c2-46f9-92c1-336fe2b13a80)

google result.
![image](https://github.com/ananthan05/Android-Security/assets/140697378/595891ad-d6e6-4b6a-a185-2d1e7e3d8a69)

