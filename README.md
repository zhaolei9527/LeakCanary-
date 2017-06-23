# LeakCanary-
<h5>OOM 是 Android 开发中常见的问题，而内存泄漏往往是罪魁祸首。</h5>
<h5>为了简单方便的检测内存泄漏，Square 开源了 LeakCanary，它可以实时监测 Activity 是否发生了泄漏，一旦发现就会自动弹出提示及相关的泄漏信息供分析。</h5>
<h2> LeakCanary 使用方式</h2>

为了将 LeakCanary 引入到我们的项目里，我们只需要做以下两步：<br><br><br>
dependencies {<br>
  &nbsp;        &nbsp;     &nbsp;     &nbsp;     debugCompile 'com.squareup.leakcanary:leakcanary-android:1.5.1'<br>
   &nbsp;       &nbsp;     &nbsp;     &nbsp;     releaseCompile 'com.squareup.leakcanary:leakcanary-android-no-op:1.5.1'<br>
   &nbsp;       &nbsp;     &nbsp;     &nbsp;     testCompile 'com.squareup.leakcanary:leakcanary-android-no-op:1.5.1'<br>
    }<br><br><br>
public class ExampleApplication extends Application {<br>
        &nbsp;     &nbsp;       @Override public void onCreate() {<br>
    &nbsp;     &nbsp;     &nbsp;        super.onCreate();<br>
    &nbsp;     &nbsp;     &nbsp;     &nbsp;     &nbsp;       if (LeakCanary.isInAnalyzerProcess(this)) {<br>
    &nbsp;       &nbsp;     &nbsp;     &nbsp;     &nbsp;        // This process is dedicated to LeakCanary for heap analysis.<br>
    &nbsp;       &nbsp;     &nbsp;     &nbsp;     &nbsp;         // You should not init your app in this process.<br>
   &nbsp;     &nbsp;      &nbsp;     &nbsp;     &nbsp;     &nbsp;     &nbsp;         return;<br>
  &nbsp;       &nbsp;     &nbsp;     &nbsp;     &nbsp;      }<br>
    &nbsp;     &nbsp;     &nbsp;     &nbsp;       LeakCanary.install(this);<br>
    &nbsp;     &nbsp;     &nbsp;     &nbsp;         }<br>
        &nbsp;     &nbsp;       }<br>
最关键的就是 LeakCanary.install(this); 这么一句话，正式开启了 LeakCanary 的大门，未来它就会自动帮我们检测内存泄漏，并在发生泄漏是弹出通知信息。
