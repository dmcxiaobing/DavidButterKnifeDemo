# DavidButterKnifeDemo
【Android】Android开发之著名框架ButterKnife的使用详解，butterknife8.1.0版本的使用方法
作者：程序员小冰 （转载请说明出处）博客地址：http://blog.csdn.net/qq_21376985

长期维护的Android项目，里面包括常用功能实现，以及知识点详解， 当然还有Java中的知识点。

具体请看github：`https://github.com/QQ986945193/DavidAndroidProjectTools`

简单介绍一下，butterknife是一款非常著名的开源框架，省去了findViewById来初始化控件。

这里只介绍AndroidStudio使用方法，eclipse请自行搜索或者看官方资料。

butterknife是由Android大神JakeWharton所开发，项目地址

```
https://github.com/JakeWharton/butterknife/
```

这里说一下8.1.0版本的使用，这个版本和以前的老版本使用方法修改了一下，不过也是比较简单的。

首先我们要在Module中build.gradle增加引入库：

```
    /*增加注解的使用 butterknife*/
    compile 'com.jakewharton:butterknife:8.1.0'
    apt 'com.jakewharton:butterknife-compiler:8.1.0'//增加这一句
```

还有Module中build.gradle添加构建：

```
apply plugin: 'android-apt'
```

然后我们需要在Project中build.gradle的depencises添加：

```
 classpath 'com.neenbedankt.gradle.plugins:android-apt:1.8' 
```

然后最后我们就可以使用我们的butterknife了。简单写一下Activity的使用：

```
   @BindView(R.id.tv)
    TextView tv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ButterKnife.bind(this);
    }
```
fragment中看官方使用了解绑，我在这里这样使用：

```
 /**
     * ButterKnife的使用，官方在fragment中使用了解绑
     */
    protected Unbinder unbinder;
    @BindView(R.id.tv)
    TextView tv;

    @Nullable
    @Override
    public View onCreateView(LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View rootView = inflater.inflate(R.layout.activity_main, container, false);
        unbinder = ButterKnife.bind(this, rootView);
        return rootView;
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        unbinder.unbind();
    }
```

好了，教程到此结束。是不是很简单呢?一次配置，多次使用。

本节示例源代码地址：https://github.com/QQ986945193/DavidButterKnifeDemo.git
