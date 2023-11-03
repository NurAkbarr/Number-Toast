# **Number Toast**

```
Nama    : Nurul Akbar
NIM     : 312210413
Kelas   : TI.22.A4
Matkul  : Pemograman Mobile
```

# **Deskripsi**

# String

- String adalah tipe data yang sangat umum digunakan dalam pemrograman, termasuk dalam pengembangan aplikasi Android dengan Android Studio. Fungsi string pada Android Studio adalah untuk memanipulasi dan mengelola teks atau data dalam bentuk karakter.

```xml
<resources>
    <string name="app_name">Hello</string>
    <string name="button_count">Count</string>
    <string name="button_toast">Toast</string>
    <string name="fibonacci_message">Program Fibonacci</string>
</resources>
```

# Color

- Di Android Studio, Anda dapat menggunakan berbagai fungsi dan mekanisme yang berkaitan dengan pengelolaan warna (color) untuk mengubah tampilan antarmuka pengguna (UI) dalam aplikasi Android.

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
    <color name="colorNumber">#BE8728</color>
    <color name="colorFibonacciBlue">#0000FF</color>
    <color name="colorFibonacciRed">#D14114</color>
    <color name="colorFibonacciOrange">#FF5722</color>
    <color name="purple">#7453AF</color>
</resources>
```

# Main Acivity

- Dalam pengembangan aplikasi Android menggunakan Android Studio, "MainActivity" adalah aktivitas pertama yang akan diluncurkan ketika aplikasi Anda dijalankan. Aktivitas ini berperan penting dalam mengatur antarmuka pengguna (UI) dan logika utama aplikasi Anda. Biasanya, Anda akan menulis kode yang berkaitan dengan MainActivity di dalam berkas MainActivity.java. Ini adalah tempat di mana Anda menginisialisasi elemen UI, menangani interaksi pengguna, dan mengelola alur kerja aplikasi Anda.

```java
package com.helloapp;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.content.ContextCompat;

import android.os.Bundle;
import android.widget.TextView;
import android.view.View;
import android.widget.Toast;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {

    private long fibMinus1 = 0;
    private long fibMinus2 = 1;
    private long currentFib = 0;
    private TextView showCount;
    private long n = 0;
    private long limit = 0;

    private EditText mLimitInput;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        showCount = (TextView) findViewById(R.id.show_count);
        mLimitInput = (EditText) findViewById(R.id.limit_input);
        updateFibonacciDisplay();
    }

    public void countUp(View view) {
        if (mLimitInput.getText().toString().isEmpty()) {
            Toast.makeText(this, "Enter the limit first", Toast.LENGTH_SHORT).show();
            return;
        }

        limit = Long.parseLong(mLimitInput.getText().toString());

        if (currentFib >= limit) {
            Toast.makeText(this, "Fibonacci limit reached", Toast.LENGTH_SHORT).show();
            return;
        }

        long newFib = fibMinus1 + fibMinus2;
        fibMinus2 = fibMinus1;
        fibMinus1 = newFib;
        currentFib = newFib;
        n++;

        if (currentFib >= limit) {
            Toast.makeText(this, "Fibonacci limit reached", Toast.LENGTH_SHORT).show();
            return;
        }

        updateFibonacciDisplay();
    }

    public void showToast(View view) {
        Toast toast = Toast.makeText(this, R.string.fibonacci_message, Toast.LENGTH_SHORT);
        toast.show();
    }

    public void reset(View view) {
        currentFib = 0;
        fibMinus2 = 1;
        fibMinus1 = 0;
        limit = 0;
        n = 0;
        mLimitInput.setText(""); // Clear the input
        updateFibonacciDisplay();
    }

    private void updateFibonacciDisplay() {
        if (showCount != null) {
            showCount.setText(Long.toString(currentFib));
            showCount.setTextColor(getFibonacciColor());
        }
    }

    private int getFibonacciColor() {
        // Change color based on the Fibonacci value
        if (n % 2 == 0) {
            return ContextCompat.getColor(this, R.color.colorFibonacciBlue);
        } else {
            return ContextCompat.getColor(this, R.color.colorFibonacciOrange);
        }
    }
}
```

# Activity

Activity pada Android Studio adalah komponen yang menyediakan antarmuka pengguna (UI) untuk aplikasi. Activity adalah satu layar di aplikasi Android, dan setiap activity memiliki layout sendiri. Activity dapat berisi berbagai elemen UI, seperti tombol, teks, gambar, dan video. Activity adalah komponen penting dari aplikasi Android. Activity digunakan untuk menampilkan informasi kepada pengguna dan menerima input dari pengguna. Activity juga dapat digunakan untuk memulai aktivitas lain, menjalankan layanan, dan melakukan tugas-tugas lainnya.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    tools:context="MainActivity">
```

# Button Toast

```xml
<Button
        android:id="@+id/button_toast"
        android:layout_width="165dp"
        android:layout_height="49dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:background="@color/colorPrimary"
        android:onClick="Toast"
        android:text="@string/button_toast"
        android:textColor="@android:color/white"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="OnClick" />
```

# EditText

```xml
<EditText
        android:id="@+id/limit_input"
        android:layout_width="162dp"
        android:layout_height="46dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:background="@color/purple"
        android:hint="limit"
        android:inputType="number"
        android:textAlignment="center"
        android:textColor="@color/white"
        android:textColorHint="@color/white"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

# Button Count

```xml
 <Button
        android:id="@+id/button_count"
        android:layout_width="173dp"
        android:layout_height="42dp"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="4dp"
        android:background="@color/colorPrimary"
        android:onClick="countUp"
        android:text="@string/button_count"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent" />
```

# Button Riset

```xml
 <Button
        android:id="@+id/button_reset"
        android:layout_width="161dp"
        android:layout_height="42dp"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="4dp"
        android:background="@color/colorPrimary"
        android:onClick="reset"
        android:text="Reset"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        tools:ignore="OnClick" />
```

# TextView

```xml
   <TextView
        android:id="@+id/show_count"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginBottom="8dp"
        android:background="#FFFF00"
        android:gravity="center_vertical"
        android:text="0"
        android:textAlignment="center"
        android:textColor="@color/colorPrimary"
        android:textSize="160sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@+id/button_count"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/button_toast"
        app:layout_constraintVertical_bias="0.0"
        tools:ignore="RtlCompat" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

# **Output**

- Sebelum memulai kita harus memasukkan limit terlebih dahulu 

![img](https://github.com/NurAkbarr/Number-Toast/blob/74ed9a3437b4512f37f5a5eaeac9985be4a4f9b6/assets/1.png)
![img](https://github.com/NurAkbarr/Number-Toast/blob/74ed9a3437b4512f37f5a5eaeac9985be4a4f9b6/assets/2.png)
![img](https://github.com/NurAkbarr/Number-Toast/blob/74ed9a3437b4512f37f5a5eaeac9985be4a4f9b6/assets/3.png)
![img](https://github.com/NurAkbarr/Number-Toast/blob/74ed9a3437b4512f37f5a5eaeac9985be4a4f9b6/assets/4.png)
![img](https://github.com/NurAkbarr/Number-Toast/blob/74ed9a3437b4512f37f5a5eaeac9985be4a4f9b6/assets/5.png)
![img](https://github.com/NurAkbarr/Number-Toast/blob/74ed9a3437b4512f37f5a5eaeac9985be4a4f9b6/assets/6.png)