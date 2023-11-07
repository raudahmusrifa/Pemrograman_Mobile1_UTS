# Repository ini dibuat untuk memenuhi penilaian Ujian Tengah Semester

Nama : Raudah Musrifa

Nim : 312210020

Kelas : TI.22.B1

Mata Kuliah : Pemrograman Mobile 1

Tugas : Membuat tombol yang setiap diklik dapat bertambah angkanya dengan urutan angka fibonacci dilengkapi dengan fitur toast
berikut adalah link video aplikasi yang di jalankan: [tonton video](https://youtu.be/_ZgtVoJHxu0)

Source Code:

- activity_main.Xml 

(dibuat dengan design pada android studio):

      <?xml version="1.0" encoding="utf-8"?>
      <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
          android:layout_width="match_parent"
          android:layout_height="match_parent">
          <LinearLayout
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:gravity="center"
              android:background="#eeeeee"
              android:orientation="vertical"
              android:paddingLeft="40dp"
              android:paddingRight="40dp">
      
              <TextView
                  android:id="@+id/textView2"
                  android:layout_width="match_parent"
                  android:layout_height="wrap_content"
                  android:layout_marginTop="10dp"
                  android:text="Increment"
                  android:textAlignment="center"
                  android:textSize="24sp" />
      
              <TextView
                  android:id="@+id/textViewNumber"
                  android:layout_width="match_parent"
                  android:layout_height="wrap_content"
                  android:layout_marginTop="10dp"
                  android:text="0"
                  android:textAlignment="center"
                  android:textSize="24sp" />
      
              <TextView
                  android:id="@+id/textView"
                  android:layout_width="match_parent"
                  android:layout_height="wrap_content"
                  android:layout_marginTop="10dp"
                  android:text="Fibonnaci"
                  android:textAlignment="center"
                  android:textSize="24sp" />
      
              <TextView
                  android:id="@+id/textViewNumberFibo"
                  android:layout_width="match_parent"
                  android:layout_height="wrap_content"
                  android:layout_marginTop="10dp"
                  android:text="0"
                  android:textFontWeight="600"
                  android:textColor="@color/black"
                  android:textAlignment="center"
                  android:textSize="24sp" />
          </LinearLayout>
      
          <Button
              android:id="@+id/button_toast"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:layout_alignParentBottom="true"
              android:layout_alignParentLeft="true"
              style="@style/Widget.AppCompat.Button"
              android:text="Toast" />
          <Button
              android:id="@+id/button_reset"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="Reset"
              android:layout_margin="10dp"
              android:backgroundTint="@color/red"
              android:textColor="@color/white"
              android:textAlignment="center" />
          <Button
              android:id="@+id/button_hitung"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:layout_alignParentBottom="true"
              android:layout_alignParentRight="true"
              android:backgroundTint="@color/teal_700"
              android:layout_marginRight="10dp"
              android:textColor="@color/white"
              android:text="Hitung" />
      
      </RelativeLayout>

Penjelasan :

1. kita isi relative layout dengan 2 linear layout

2. linear layout1 diisi dengan 3 textview:

    - nama + nim
    
    - jumlah klik pada tombol hitung
    
    - angka fibonacci terakhir

3. linear layout 2 berisi :

    - button hitung
    
    - button reset
    
    - button toast

- MainActivity.Java :

        package com.example.belajarandroidti22b1;
        
        import androidx.appcompat.app.AppCompatActivity;
        
        import android.os.Bundle;
        import android.view.View;
        import android.widget.Button;
        import android.widget.TextView;
        
        import androidx.appcompat.app.AppCompatActivity;
        
        import android.os.Bundle;
        import android.view.View;
        import android.widget.Button;
        import android.widget.TextView;
        import android.widget.Toast;
        
        public class MainActivity extends AppCompatActivity {
            private int mCount = 0;
            private int mCountFibo = 0;
            private TextView mShowCount;
            private TextView mShowCountFibo;
            private Button buttonToast;
            private Button buttonHitung;
            private Button buttonReset;
        
            @Override
            protected void onCreate(Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.activity_main);
                mShowCount = (TextView) findViewById(R.id.textViewNumber);
                mShowCountFibo = (TextView) findViewById(R.id.textViewNumberFibo);
                buttonToast = (Button) findViewById(R.id.button_toast);
                buttonHitung = (Button) findViewById(R.id.button_hitung);
                buttonReset = (Button) findViewById(R.id.button_reset);
        
                buttonHitung.setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {hitungIncrement(view);}
                });
                buttonToast.setOnClickListener(new View.OnClickListener(){
                    @Override
                    public void onClick(View view) {showToast(view);}
                });
                buttonReset.setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {resetCountDanFibbo(view);}
                });
            }
        
            public void showToast(View view){
                Toast toast = Toast.makeText(this, R.string.toast_pesan, Toast.LENGTH_SHORT);
                toast.show();
            }
        
            public void hitungIncrement(View view) {
                mCount++;
                int fibo = hitungFibonacci(mCount);
                mCountFibo = fibo;
                if (mShowCount != null && mShowCountFibo != null) {
                    mShowCount.setText(Integer.toString(mCount));
                    mShowCountFibo.setText(Integer.toString(mCountFibo));
                }
            }
        
            public int hitungFibonacci(int n){
                if(n <= 1){
                    return n;
                }
                int prev = 0;
                int current = 1;
                for(int i = 2; i <= n; i++){
                    int next = prev + current;
                    prev = current;
                    current = next;
                }
                return current;
            }
        
            public void resetCountDanFibbo(View view){
                mCount = 0;
                mCountFibo = 0;
                mShowCount.setText(Integer.toString(mCount));
                mShowCountFibo.setText(Integer.toString(mCountFibo));
            }
        }

- strings.xml
  
(Tipe data teks)

    <resources>
        <string name="app_name">BelajarAndroid</string>
        <string name="button_label_toast">Toast</string>
        <string name="button_label_hitung">Hitung</string>
        <string name="hitung_initial_value">0</string>
        <string name="toast_pesan">Berhasil diklik</string>
    </resources>

- colors.xml

  (Menambahkan warna pada program)

      <?xml version="1.0" encoding="utf-8"?>
      <resources>
          <color name="black">#FF000000</color>
          <color name="white">#FFFFFFFF</color>
          <color name="biru">#0000FF</color>
          <color name="colorPrimary">#3F51B5</color>
          <color name="colorPrimaryDark">#303F9F</color>
          <color name="colorAccent">#FF4081</color>
          <color name="kuning">#FFFF00</color>
          <color name="red">#D10000</color>
          <color name="teal_700">#FF018786</color>
      </resources>

  Selesai, terimakasih



  

  










