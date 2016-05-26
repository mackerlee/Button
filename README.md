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
      <Button
        android:id="@+id/Button06"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/Button06"
        android:drawableLeft="@drawable/ic_android_16px"
        //--设置透明按钮，?表示查找,在其后的android中查找，固定写法,如果没有查找到则按原来的样式显示
        style="?android:attr/borderlessButtonStyle"   //按钮没有边框，透明的
        android:text="透明样式的按钮"/>
      <Button
        android:id="@+id/Button07"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/Button06"
        //--绑定图片选择器
        android:background="@drawable/button_custom"
        android:text="自定义背景的按钮"/>  
        
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

4.内部类在运行时会产生内存的额外开销，建议采用方式五自定义方式或方式二实现接口
5.Nine-patch位图：在拉升时，该变的地方会变，不该变的也不会扭曲变形的图片.它仍然是一个png格式的图片，只不过是针对Android平台的                   可以指定图片特定位置拉伸和填充内容的一种特殊的png图片格式，通常用于按钮背景,设置按钮图片背景实例:
  在res->drawable下创建图片选择器button_custom.xml,绑定按钮button07(上面activity_main.xml中定义)
  <?xml version="1.0" encoding="utf-8"?>
  <selector xmlns:android="http://schemas.android.com/apk/res/android">
      //--以下三个选择用于选择显示按钮在不同状态下的显示图片
      <item android:drawable="@drawable/button_pressed"     //按钮按下时显示
          android:state_pressed="true" />
      <item android:drawable="@drawable/button_focused"     //按钮获取到焦点时显示的图片
          android:state_focused="true" />
      <item android:drawable="@drawable/button_default" />  //按钮默认情况下显示的图片
  </selector>
  
android 47-48 lessones
1.ImageView组件:专门用于显示图片的组件,继承view，它可以加载图像从不同来源，负责计算图像的测量，这样它就可以用于任意布局管理                   器，并提供各种显示选项如缩放和上色.
2.ImageView组件的XML属性:
  --android:src：设置View的drawable图片位置;
  --android:adjustViewBounds：是否保持宽高比,需要与maxWidth/MaxHigt一起使用，否则单独使用没有效果
  --android:maxHight/maxWidth：设置View的最大值，单独使用无效,要和adjustViewBounds一起使用,如果想设置图片固定大小又要保持图                                片宽高比，需要如下设置：
                                  设置setAdjustViewBounds为true
                                  设置maxWidth/maxHeight值
                                  设置layout_width和layout_height为wrap_content
  --android:scaleType：设置图片的填充方式,用类该属性则adjustViewBounds/maxHight/maxWidth就不需要设置了，但将layout_width和layo                       ut_height为wrap_content设置成具体数值来配合使用，有以下几种方式：
                      --matrix：用矩阵来绘图
                      --fitXY：拉伸图片（不按比例）以填充View的宽高
                      --fitStart：按比例拉伸，拉伸后图片的高度为View的高度，且显示在View的上边;
                      --fitCenter：按比例拉伸，拉伸后图片的高度为View的高度，且显示在View的中间;
                      --fitEnd：按比例拉伸，拉伸后图片的高度为View的高度，且显示在View的下边;
                      --center：按原图大小显示图片, 但图片宽高大于View的宽高时，截取图片中间部分显示;
                      --centerCrop：按比例缩放原图直到等于某个View的宽高显示,
                      --centerInside：当原图宽高或等于View的宽高时,按原图大小剧中显示,反之将原图缩放至View的宽高居中显示
                      
3.ImageView实例：在res->layout->imageview_activity_main.xml中：
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:layout_width="match_parent"
      android:layout_height="match_parent">
  
      <ImageView
          android:id="@+id/imageview01"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:src="@drawable/bb1"
          android:maxWidth="200dp"
          android:maxHeight="300dp"
          //--如果adjustViewBounds设置为true则以maxheight和maxwidth中最小值为准按比例缩放，如果adjustViewBounds为false则按原图显示
          android:adjustViewBounds="true"/>
      <ImageView
        android:id="@+id/imageview02"
        android:layout_width="150dp"
        android:layout_height="300dp"
        android:layout_below="@id/imageview01"
        android:src="@drawable/bb2"
        android:scaleType="centerCrop"/>
    <ImageButton //其设置样式/响应方式与Button一样
        android:id="@+id/imagebutton01"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/imageview02"
        android:src="@drawable/ic_android"/>
  </RelativeLayout>

4.ImageButton:图像按钮

