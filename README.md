## **Repositori ini dibuat untuk memenuhi penilaian tengah semester matakuliah pemrograman mobile**  
Nama : GARNISH ANDHIKA PRATAMA  
Nim : 312210161  
Kelas : TI.22.B1  
Mata Kuliah : Pemrograman Mobile (TUGAS UTS) 
**Tugas : Membuat tombol yang setiap diklik dapat bertambah angkanya, namun dengan urutan angka fibonacci, lalu lengkapi dengan fitur toast**  
berikut adalah link video aplikasi yang di jalankan (dijalankan pada device menggunakan usb debugging) : [tonton video](https://www.youtube.com/shorts/Fj5d-t8HxHg)  
<br>
Source Code:  
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:gravity="center"
        android:background="@color/grey"
        android:paddingLeft="40dp"
        android:paddingRight="40dp">

        <TextView
            android:id="@+id/textView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:text="Increment"
            android:textAlignment="center"
            android:textSize="24sp"/>

        <TextView
            android:id="@+id/textView2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:text="0"
            android:textAlignment="center"
            android:textSize="24sp"/>

        <TextView
            android:id="@+id/textView3"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:text="Fibonacci"
            android:textAlignment="center"
            android:textSize="24sp"/>

        <TextView
            android:id="@+id/textView4"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:text="0"
            android:textAlignment="center"
            android:textFontWeight="600"
            android:textSize="24sp"/>


    </LinearLayout>

    <Button
        android:id="@+id/button_toast"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_alignParentBottom="true"
        android:layout_marginLeft="20dp"
        android:layout_marginBottom="15dp"
        android:backgroundTint="@color/blue"
        android:textColor="@color/white"
        android:text="Toast"/>
    <Button
        android:id="@+id/button_reset"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Reset"
        android:layout_marginTop="20dp"
        android:backgroundTint="@color/Red"
        android:textColor="@color/white"
        android:layout_marginLeft="10dp"
        android:textAlignment="center"/>

    <Button
        android:id="@+id/button_hitung"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hitung"
        android:layout_marginBottom="15dp"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:layout_marginRight="20dp"
        android:backgroundTint="@color/blue"
        android:textColor="@color/white"/>
</RelativeLayout>

Penjelasan :  
1. kita isi relative layout dengan 2 linear layout
2. linear layout1 diisi dengan 3 textview:
   * nama + nim
   * jumlah klik pada tombol hitung
   * angka fibonacci terakhir
3. linear layout 2 berisi :
   * button hitung
   * button reset
   * dan button toast  



* MainActivity.Java :  

``` java
package ic.co.toats;

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
        setContentView(R.layout.toast_activity);
        mShowCount = (TextView) findViewById(R.id.textView2);
        mShowCountFibo = (TextView) findViewById(R.id.textView4);
        buttonToast = (Button) findViewById(R.id.button_toast);
        buttonHitung = (Button) findViewById(R.id.button_hitung);
        buttonReset = (Button) findViewById(R.id.button_reset);

        buttonHitung.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) { hitungIncrement(view);}

        });
        buttonToast.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View view) {showToast(view);}
        });
        buttonReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) { resetCountDanFibbo(view);}
        });
    }


    public void showToast(View view){
        Toast toast = Toast.makeText(this, "Berhasil DiKlik",Toast.LENGTH_SHORT);
        toast.show();
    }

    public void hitungIncrement(View view){
        mCount++;
        int fibo = hitungFibonacci(mCount);
        mCountFibo =fibo;
        if(mShowCount != null && mShowCountFibo != null){
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
```

penjelasan MainActivity.java :   
``` Java
    public int count = 0 ;
    public int countFibo = 0 ;
    public TextView showCount;
    public TextView showCountFibo;
    public Button buttonToast;
    public Button buttonCount;
    public Button buttonReset;
    public Toast toastA;
```  
* kita deklarasikan properti atau atribut yang akan kita gunakan dalam aplikasi ini
* untuk count dan countFibo langsung kita isi dengan nilai 0 (integer)
* masing masing diberi sesuai tipe data dan kita set visibility nya public
<br> <br> <br>
```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        buttonToast=(Button)findViewById(R.id.buttonToast);
        buttonCount=(Button)findViewById(R.id.buttonCount);
        buttonReset=(Button)findViewById(R.id.buttonReset);
        showCount =(TextView)findViewById(R.id.textCount);
        showCountFibo =(TextView)findViewById(R.id.textCountFibo);


        buttonToast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(toastA != null) { toastA.cancel(); }
                    toastA = Toast.makeText(getApplicationContext(), "Angka Fibonacci : " + countFibo, Toast.LENGTH_SHORT);
                    toastA.show();
            }
        });

        buttonCount.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) { calculate(view); }
        });

        buttonReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) { reset(view); }
        });


    }
```
* disini kita akan mengisi beberapa properti yang belum diisi sebelumnya sesuai dengan tipe data
* lalu dihubungkan menggunakan tipe data dan juga id yang ada ada activity_main.xml
* kemudian kita beri event atau aksi yang akan dilakukan ketika tombol tombol diklik
* saat tombol hitung diklik maka akan menjalankan fungsi calculate
* saat tombol reset diklik maka akan menjalankan fungsi reset
* saat tombol tampilkan toast diklik maka akan menampilkan toast dengan data angka fibonacci
  <br> <br>

```java
    protected void calculate(View view){
        count++;
        countFibo = calculateFibo(count);
        showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
        if(count % 5 == 0){
            if(toastA != null) toastA.cancel();
            toastA = Toast.makeText(getApplicationContext(),"Tombol hitung diklik : "+ count + " Kali", Toast.LENGTH_SHORT);
            toastA.show();
        }
    }
```
* saat fungsi dijalankan, maka akan menambah properti count dengan nilai 1
* kemudian count yang sudah ditambah , maka akan dijadikan nilai dalam menjalankan fungsi calculateFibo lalu akan menerima data baru yang telah diolah di fungsi tersebut dan kemusian dimasukkan ke properti countFibo
* tampilkan jumlah klik tombol hitung dan juga angka fibonacci
* kita tampilkan toast setiap tombol count diklik sebanyak 5 kali
* untuk toastA.cancel() bermaksud agar toast yang sudah ada langsung dihentikan karena toast paling cepat akan hilang dalam dua detik, jika belum dua detik dan ada toast yang aktif maka toast yang baru akan masuk dalam antrian, dan akan dijalankan berurut setelah dua detik dengan cancel ini maka kita hentikan toast yang ada
* lalu jalankan toast.show() agar langsung kita tampilkan toast yang baru
<br> <br> <br>

```java
    protected int calculateFibo(int n){
        if(n <= 1) return n;
        int prev,current,next;
        prev = 0;
        current = 1;
        for (int i = 2; i <= n; i++) {
            next = prev + current;
            prev = current;
            current = next;
        }
        return current;
    }
```
* di fungsi calculateFibo angka count yang dikirimkan dari fungsi calculate akan diolah sehingga akan me return angka fibonacci
<br> <br> <br>

```java
protected void reset(View view){
        count = 0;
        countFibo = 0;
        showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
    }
```
* disini semua properti angka dan textview akan direset
