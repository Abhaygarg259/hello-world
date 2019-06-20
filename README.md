# hello-world
//code for live api called by the android studio

main activity page
package com.example.news1;


import android.os.Bundle;

import com.google.android.material.floatingactionbutton.FloatingActionButton;
import com.google.android.material.snackbar.Snackbar;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;

import android.view.View;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.ArrayAdapter;
import android.widget.Spinner;


import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;




public class MainActivity extends AppCompatActivity {

    public static void main(String[] args) {
        try{

            URL u= new URL ("https://www.digitaltrends.com/dtdeals/best-apple-deals-for-prime-day");
            HttpURLConnection hr=(HttpURLConnection)u.openConnection();
            if (hr.getResponseCode()==200){
                InputStream im=hr.getInputStream() ;
                StringBuffer sb=new StringBuffer() ;
                BufferedReader br=new BufferedReader(new InputStreamReader(im) ) ;
                FileOutputStream fo=new FileOutputStream("");
                BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(fo));
                String line=br.readLine() ;
                while (line!=null ) {
                    System.out.println(line);
                    bw.write(line);
                    bw.newLine();
                    line=br.readLine() ;
                }

            }

        }catch (Exception  e){
            System.out.println(e);
        }

    }



    @Override
    protected void onCreate(Bundle savedInstanceState) {


        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        Spinner spinner = (Spinner) findViewById(R.id.spinner);
        ArrayAdapter<String> adapter;
        List<String> list;
        list = new ArrayList<String>();
        list.add("International");
        list.add("National");
        list.add("Sports");
        boolean weather = list.add("Weather");
        adapter = new ArrayAdapter<String>(getApplicationContext(),
                android.R.layout.simple_spinner_item, list);
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        spinner.setAdapter(adapter);
        FloatingActionButton fab = findViewById(R.id.fab);
        fab.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();
            }
        });
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.menu_main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }


        return super.onOptionsItemSelected(item);
    }
}

