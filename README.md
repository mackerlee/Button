# Button

android 44-45 lessones
1.Button:也是TextView的子类，点击由用户来执行一个动作.
2.Button实例：在res->layout->activity_main.xml中定义Button
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:paddingBottom="@dimen/activity_vertical_margin"
      android:paddingLeft="@dimen/activity_horizontal_margin"
      android:paddingRight="@dimen/activity_horizontal_margin"
      android:paddingTop="@dimen/activity_vertical_margin"
      tools:context="com.example.mackerlee.android_44.MainActivity">
  
      <Button
        android:id="@+id/Button01"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:drawableLeft="@drawable/ic_android_16px"
        android:text="匿名内部类实现的事件处理"/>
      <Button
          android:id="@+id/Button02"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_below="@id/Button01"
          android:drawableLeft="@drawable/ic_android_16px"
          android:text="在Activity中实现View.OnClickListener接口"/>
      <Button
          android:id="@+id/Button03"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_below="@id/Button02"
          android:drawableLeft="@drawable/ic_android_16px"
          android:text="创建实例化接口对象实现方式"/>
      <Button
          android:id="@+id/Button04"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_below="@id/Button03"
          android:drawableLeft="@drawable/ic_android_16px"
          android:text="使用内部类的方式事件触发"/>
      <Button
          android:id="@+id/Button05"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_below="@id/Button04"
          android:drawableLeft="@drawable/ic_android_16px"
          //--设置连接到MainActivity.java中自定义的按钮响应方法
          android:onClick="myOnClick"
          android:text="使用自定义方法的方式"/>
  </RelativeLayout>
3.Button触发事件:5种触发方式，在app->java->包名->MainActivity.java中:
  package com.example.mackerlee.android_44;

  import android.support.v7.app.AppCompatActivity;
  import android.os.Bundle;
  import android.view.View;
  import android.widget.Button;
  import android.widget.Toast;
  
  public class MainActivity extends AppCompatActivity implements View.OnClickListener{ //按钮触发方式二:在Activity中继承View.OnClickListener接口
  
      private Button btn1,btn2,btn3,btn4,btn5;
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          btn1 = (Button)findViewById(R.id.Button01);
  
          //--按钮触发方式一：匿名内部类
          btn1.setOnClickListener(new View.OnClickListener(){
              public void onClick(View v){
                  Toast.makeText(MainActivity.this,"匿名内部类方式实现Button事件处理",Toast.LENGTH_LONG).show();
              }
          });
  
          //--按钮触发方式二:button2链接到MainActivity的监听方法
          btn2 = (Button)findViewById(R.id.Button02);
          btn2.setOnClickListener(this);
  
          //--按钮触发方式三:直接创建实例化接口对象，并在里面实现接口方法
          btn3 = (Button)findViewById(R.id.Button03);
          View.OnClickListener listener = new View.OnClickListener(){
              @Override
              public void onClick(View v) {
                  Toast.makeText(MainActivity.this,"创建实例化接口对象方式实现",Toast.LENGTH_LONG).show();
              }
          };
          btn3.setOnClickListener(listener);  //链接上面定义的接口对象
  
          //--按钮触发方式四:内部类方式
          btn4 = (Button)findViewById(R.id.Button04);
          btn4.setOnClickListener(new MyOnClickListener()); //参数new一个内部类对象
      }
  
      //--按钮触发方式二:在Activity中实现View.OnClickListener接口方法
      @Override
      public void onClick(View v) {
          switch (v.getId()){
              case R.id.Button02:
                  Toast.makeText(MainActivity.this,"在Activity中实现View.OnClickListener接口方式",Toast.LENGTH_LONG).show();
                  break;
          }
      }
  
      //--按钮触发方式四:内部类方式,内部类继承实现View.OnClickListener
      class MyOnClickListener implements View.OnClickListener{
          @Override
          public void onClick(View v) {
              Toast.makeText(MainActivity.this,"使用内部类的方式实现事件处理",Toast.LENGTH_LONG).show();
          }
      }
  
      /**
       * 按钮触发方式五:使用自定义方式，定义一个onClick方法,名称随意取,但必须满足以下三个条件:
       * 1。必须是public
       * 2. 必须返回void
       * 3. 必须定义一个View类型的唯一的参数,这个view就是当前的button
       * 4. 然后再定义Buttond的activity_main.xml中相应的Button设置android:onClick="myOnClick"属性即可
       */
      public void myOnClick(View view){
          Toast.makeText(this,"使用自定义方法的方式",Toast.LENGTH_LONG).show();
      }
  }

4.内部类在运行时会产生内存的额外开销，
