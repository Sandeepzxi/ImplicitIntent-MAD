# Ex.No 2a: Navigate Button using Implicit Intent
 
## Aim
To create an Android application with a text field and a **Navigate** button that opens a web page (for example, `www.gmail.com`) in the browser using an **Implicit Intent**, developed in Android Studio.
 
## Equipment Required
- Latest version of Android Studio
- Android Emulator (Google APIs image with Chrome) or a physical Android device
## Concept
An **Implicit Intent** does not name a specific component to start. It declares a general action (here `Intent.ACTION_VIEW`) along with data (a URI), and the Android system finds a suitable app, usually a browser, to handle it.
 
## Algorithm
1. Start `onCreate()` and load `activity_main.xml` using `setContentView()`.
2. Find the `EditText` (id: `editText`) and `Button` (id: `btn`) using `findViewById()`.
3. Attach an `OnClickListener` to the button.
4. On click, read the text using `getText().toString().trim()`.
5. If the text is empty, show a Toast and stop.
6. If the URL does not start with `http://` or `https://`, prepend `https://`.
7. Create an implicit intent: `new Intent(Intent.ACTION_VIEW, Uri.parse(url))`.
8. Call `startActivity(intent)`, handling `ActivityNotFoundException` if no browser exists.
9. The browser opens and displays the requested page.
## Project Details
| Item | Value |
|------|-------|
| App name | ImplicitIntent |
| Package | `com.example.implicitintent` |
| Language | Java |
| Min SDK | API 24 |
| Layout | ConstraintLayout |
 
## Program
 
### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
 
    <EditText
        android:id="@+id/editText"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginEnd="24dp"
        android:hint="@string/url_hint"
        android:inputType="textUri"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.4" />
 
    <Button
        android:id="@+id/btn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:text="@string/navigate"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/editText" />
 
</androidx.constraintlayout.widget.ConstraintLayout>
```
 
### res/values/strings.xml
```xml
<resources>
    <string name="app_name">ImplicitIntent</string>
    <string name="url_hint">Enter URL (e.g. www.gmail.com)</string>
    <string name="navigate">Navigate</string>
</resources>
```
 
### MainActivity.java
```java
/*
Program to open a web page using Implicit Intent.
Developed by: SANDEEP S
Registration Number: 212223220092
*/
package com.example.implicitintent;
 
import android.content.ActivityNotFoundException;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
 
import androidx.appcompat.app.AppCompatActivity;
 
public class MainActivity extends AppCompatActivity {
 
    EditText editText;
    Button btn;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
 
        editText = findViewById(R.id.editText);
        btn = findViewById(R.id.btn);
 
        btn.setOnClickListener(view -> {
            String url = editText.getText().toString().trim();
 
            if (url.isEmpty()) {
                Toast.makeText(this, "Please enter a URL", Toast.LENGTH_SHORT).show();
                return;
            }
 
            if (!url.startsWith("http://") && !url.startsWith("https://")) {
                url = "https://" + url;
            }
 
            Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
            try {
                startActivity(intent);
            } catch (ActivityNotFoundException e) {
                Toast.makeText(this, "No browser found", Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```
 
### AndroidManifest.xml (add inside `<manifest>`, outside `<application>`)
```xml
<queries>
    <intent>
        <action android:name="android.intent.action.VIEW" />
        <data android:scheme="https" />
    </intent>
</queries>
```
 
## How to Run
1. Open Android Studio and create a new **Empty Views Activity** project with the details above.
2. Replace the contents of the files shown above.
3. Start an emulator (Google APIs image with Chrome) or connect a device.
4. Click **Run**.
5. Type `www.gmail.com` in the text field and tap **Navigate**.
## Output

<img width="1535" height="862" alt="image" src="https://github.com/user-attachments/assets/8ff7fe8a-e728-4ec7-bf42-0a20a2acd613" />

# Navigating to Gmail

<img width="1535" height="862" alt="image" src="https://github.com/user-attachments/assets/7330998e-3637-4a7b-9e65-1fc28fd7ae22" />

 
## Result
Thus, an Android application with a text field and a Navigate button was developed using an Implicit Intent to open the entered web page (Gmail) in the browser, and was executed successfully.
