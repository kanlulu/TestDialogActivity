### [Android中创建具有Dialog样式的Activity](https://blog.csdn.net/qq_36046305/article/details/85264891)

简单描述来说Dialog样式的Activity就是具有Dialog的外观和Activity的特性，我们可以把他当做一种特殊的Dialog来使用。

那么问题来了，既然有了一般的Dialog为什么还需要Dialog样式的Activity来充当Dialog？因为它本质上是一个Activity，具有了一些Dialog没有的特性：

1. 拥有自己独立的生命周期，便于管理。
2. 它是一个Activity，便于处理复杂业务。

#### 如何创建Dialog样式的Activity

可按照以下步骤依次进行：

1. 创建DialogActivity。

2. 在styles.xml文件中创建一个parent为Dialog样式的style，并设置其他属性。

   ```xml
       <style name="DialogActivityTheme" parent="Theme.AppCompat.Dialog">
           <item name="android:windowTranslucentStatus">true</item><!--透明状态栏并占用状态栏位置 -->
           <item name="android:windowIsTranslucent">true</item><!-- 半透明 -->
           <item name="android:windowBackground">@color/bg_dialog</item>
           <item name="android:backgroundDimEnabled">true</item>
           <item name="android:windowContentOverlay">@null</item>
           <item name="android:windowCloseOnTouchOutside">false</item>
           <item name="android:backgroundDimAmount">0.5</item><!-- 背景模糊的透明度 数值越小越透明-->
           <item name="android:windowIsFloating">true</item><!-- 浮现在Activity之上 -->
           <item name="windowNoTitle">true</item><!-- 无标题 -->
           <item name="android:windowAnimationStyle">@null</item><!-- 进入和退出动画 -->
       </style>
   ```

3. 在AndroidManifest文件中将Activity的Theme设置为DialogActivityTheme。

   ```xml
   <activity
             android:name=".dialog.DialogActivity"
             android:theme="@style/DialogActivityTheme" />
   ```

4. 在DialogActivity中设置布局的范围和位置。

   ```java
   setContentView(R.layout.activity_dialog);
   //设置内容占据全屏
           getWindow().setLayout(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT);
           getWindow().setGravity(Gravity.CENTER);
   ```

5. 打开和关闭DialogActivity。

   ```java
      //打开Dialog
      public void showDialogActivity(View view) {
           Intent intent = new Intent(this, DialogActivity.class);
           startActivity(intent);
       }
   
   .............
       //关闭Dialog
       public void closeDialogActivity(View view) {
           finish();
       }
   ```



   [博客地址](https://blog.csdn.net/qq_36046305/article/details/85264891)