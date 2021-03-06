# 空祖家的对话框 2.2
献给要求我们安卓照着苹果设计稿做开发的产品们（手动滑稽

<a href="https://github.com/kongzue/Dialog/">
<img src="https://img.shields.io/badge/Kongzue%20Dialog-2.2.9-green.svg" alt="Kongzue Dialog">
</a> 
<a href="https://bintray.com/myzchh/maven/dialog/2.2.9/link">
<img src="https://img.shields.io/badge/Maven-2.2.9-blue.svg" alt="Maven">
</a> 
<a href="http://www.apache.org/licenses/LICENSE-2.0">
<img src="https://img.shields.io/badge/License-Apache%202.0-red.svg" alt="License">
</a> 
<a href="http://www.kongzue.com">
<img src="https://img.shields.io/badge/Homepage-Kongzue.com-brightgreen.svg" alt="Homepage">
</a> 

多语言文档：
[English](https://github.com/kongzue/Dialog/blob/master/README-Eng.md) 


空祖家的对话框2.0拥有提供最简单的调用方式以实现消息框、选择框、输入框、等待提示、警告提示、完成提示、错误提示等弹出样式。以下是目前包含的所有对话框样式预览图：

![Kongzue's Dialog](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.0.png)

试用版可以前往 http://fir.im/kongzueDial 下载

![Kongzue's Dialog Demo](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/KongzueDialogDemoDownload.png)

本例中，包含DialogDemo（Dialog/app/）是对话框的演示项目源代码，以及Library库（Dialog/dialog/）是封装的空祖家对话框的源代码。

项目托管的Maven仓库在https://bintray.com/myzchh/maven/dialog

本项目遵循Apache-2.0开源协议，具体可参考：http://www.opensource.org/licenses/apache2.0.php

## Maven仓库或Gradle的引用方式
Maven仓库：
```
<dependency>
  <groupId>com.kongzue.dialog</groupId>
  <artifactId>dialog</artifactId>
  <version>2.2.9.4</version>
  <type>pom</type>
</dependency>
```
Gradle：
在dependencies{}中添加引用：
```
implementation 'com.kongzue.dialog:dialog:2.2.9.4'
```

若需要使用 v1 兼容库的老版本，可使用：
```
implementation 'com.kongzue.dialog:dialog:2.2.8'        //警告：不再提供更新
```

若需要降低包体积，可使用不带模糊的版本：
```
implementation 'com.kongzue.dialog:dialog:2.1.0'        //警告：不再提供更新
```

## 使用说明
1) 组件启用前请先初始化全局的风格样式，具体方法为
```
DialogSettings.type = TYPE_MATERIAL;
```

Material 风格对应 DialogSettings.TYPE_MATERIAL，

Kongzue 风格对应 DialogSettings.TYPE_KONGZUE，

iOS 风格对应 DialogSettings.TYPE_IOS

需要注意的是风格设置仅针对对话框，提示框样式不会改变。

2) 要启用 Light & Dark 黑白主题模式，请调用以下语句实现：
```
DialogSettings.tip_theme = THEME_LIGHT;         //设置提示框主题为亮色主题
DialogSettings.dialog_theme = THEME_DARK;       //设置对话框主题为暗色主题
```

具体预览图如下：
![Kongzue's Dialog Light&DarkMode](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.0_dark.png)

3) 从 2.0.4 版本开始，提供不需要悬浮窗权限，且可以跨域显示的通知功能，如下图所示：
![Kongzue's Dialog Notifaction](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.0.4_notification.png)

4) 从 2.1.0 版本开始，提供底部菜单，可以通过 com.kongzue.dialog.v2.BottomMenu 进行使用，如下图所示：
![Kongzue's Dialog BottomMenu](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.1.0_bottommenu.png)

5) 从 2.1.1 版本开始，iOS风格的对话框、提示框、底部菜单新增即时模糊效果：
![Kongzue's Dialog Blur](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.1.1_blur.png)

6) 从 2.2.3 版本开始，MessageDialog、SelectDialog、InputDialog和BottomMenu 支持自定义布局：
![Kongzue's Dialog CustomView](https://github.com/kongzue/Res/raw/master/app/src/main/res/mipmap-xxxhdpi/Kongzue%20Dialog%202.2.3_customView.png)

## 关于v2组件包
在空祖家的对话框组件中，依然保留了一代的组件库但不再推荐使用，这是为了保持兼容性，若强行使用您会看到相关类的名称上有删除线。

为了更有效率的开发，我们现在强烈推荐直接使用v2组件库，其包含的包地址为：com.kongzue.dialog.v2

### 关于模糊效果
从2.1.1版本起可使用即时模糊效果。

您可以通过以下属性设置开关：
```
DialogSettings.use_blur = true;                 //设置是否启用模糊
```
如果需要启动，还需要在您的 app 的 build.gradle 中添加以下代码：
```
android {
    ...
    defaultConfig {
        ...

        renderscriptTargetApi 19
        renderscriptSupportModeEnabled true
    }
}
```
模糊效果目前仅对当 DialogSettings.type = TYPE_IOS 时三种对话框、提示框、等待框以及底部菜单有效。

### 调用消息对话框的方法：
```
MessageDialog.show(me, "消息提示框", "用于提示一些消息", "知道了", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
    }
});
```
或者可以采用快速调用方式：
```
MessageDialog.show(me, "欢迎", "欢迎使用Kongzue家的对话框，此案例提供常用的几种对话框样式。\n如有问题可以在https://github.com/kongzue/Dialog提交反馈");
```

### 调用选择对话框的方法：
```
SelectDialog.show(me, "提示", "请做出你的选择", "确定", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        Toast.makeText(me, "您点击了确定按钮", Toast.LENGTH_SHORT).show();
    }
}, "取消", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        Toast.makeText(me, "您点击了取消按钮", Toast.LENGTH_SHORT).show();
    }
});
```
或者可以采用快速调用方式：
```
SelectDialog.show(me, "提示", "请做出你的选择", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        Toast.makeText(me, "您点击了确定按钮", Toast.LENGTH_SHORT).show();
    }
});
```

### 调用输入对话框：
```
InputDialog.show(me, "设置昵称", "设置一个好听的名字吧", "确定", new InputDialogOkButtonClickListener() {
    @Override
    public void onClick(Dialog dialog, String inputText) {
        Toast.makeText(me, "您输入了：" + inputText, Toast.LENGTH_SHORT).show();
    }
}, "取消", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

    }
});
```
或者可以采用快速调用方式：
```
InputDialog.show(me, "设置昵称", "设置一个好听的名字吧", new InputDialogOkButtonClickListener() {
                    @Override
                    public void onClick(Dialog dialog, String inputText) {
                        Toast.makeText(me, "您输入了：" + inputText, Toast.LENGTH_SHORT).show();
                    }
                });
```

### 调用等待提示框：
```
WaitDialog.show(me, "载入中...");
```

### 调用完成提示框：
```
TipDialog.show(me, "完成", TipDialog.SHOW_TIME_SHORT, TipDialog.TYPE_FINISH);
```

### 调用警告提示框：
```
TipDialog.show(me, "请输入密码", TipDialog.SHOW_TIME_SHORT, TipDialog.TYPE_WARNING);
```

### 调用错误提示框：
```
TipDialog.show(me, "禁止访问", TipDialog.SHOW_TIME_LONG, TipDialog.TYPE_ERROR);
```

### 调用消息通知：

注意，此处使用的是来自com.kongzue.dialog.v2 的 Notification 类。

通知消息（v2.Notification）与提示框（v2.TipDialog）的主要区别是提示框会打断用的操作，而消息通知不会，消息通知适合于并发需要提醒用户是否处理消息的业务场景，而提示框适用于阻断用户操作，提醒用户当前发生的情况的业务场景。

```
Notification.show(me, id, iconResId, getString(R.string.app_name), "这是一条消息", Notification.SHOW_TIME_LONG, notifactionType)
                        .setOnNotificationClickListener(new Notification.OnNotificationClickListener() {
                            @Override
                            public void OnClick(int id) {
                                Toast.makeText(me,"点击了通知",SHOW_TIME_SHORT).show();
                            }
                        })
                ;
```
其中，id为通知消息id，在用户点击该通知后，会在OnNotificationClickListener中进行回调。

字段 | 含义 | 是否必须
---|---|---
context | 上下文索引 | 必须
iconResId | 图标 | 可选
title | 通知标题 | 可选
message | 通知内容 | 必须
colorType | 消息类型 | 必须
OnNotificationClickListener | 下载监听器 | 可选

注意，此处的消息类型 colorType 目前仅对“Kongzue 风格”有效，且提供的风格有：

字段 | 含义 | 是否默认
---|---|---
TYPE_NORMAL | 默认灰黑色 | 默认
TYPE_FINISH | 绿色 | 可选
TYPE_WARNING | 橙色 | 可选
TYPE_ERROR | 红色 | 可选

在2.0.6版本后，若 colorType 不为上述设定值，则可以使用自选颜色值，可为 Color 类的返回值。

另外，可以采用快速调用方式：
```
Notification.show(me, 0, "", "这是一条消息", Notification.SHOW_TIME_SHORT, notifactionType);
```

### 调用底部菜单：

注意，此处使用的是来自com.kongzue.dialog.v2 的 BottomMenu 类。
```
List<String> list = new ArrayList<>();
list.add("菜单1");
list.add("菜单2");
list.add("菜单3");
BottomMenu.show(me, list, new OnMenuItemClickListener() {
    @Override
    public void onClick(String text, int index) {
        Toast.makeText(me,"菜单 " + text + " 被点击了",SHOW_TIME_SHORT).show();
    }
},true);
```
包含的参数如下：

字段 | 含义 | 是否必须
---|---|---
activity | 必须继承自 AppCompatActivity  | 必须
list | 泛型为 String 的列表 | 必须
OnMenuItemClickListener | 点击回调 | 可选
isShowCancelButton | 是否显示“取消”按钮，注意，TYPE_MATERIAL 风格对此无效 | 可选
cancelButtonCaption | 设置“取消”按钮的文字 | 可选

另外，本菜单暂时对夜间模式（THEME_DARK）不受影响，只提供Light Theme，但不排除接下来的版本对此更新。

使用 iOS 主题时，DialogSettings.ios_normal_button_color 会对菜单内容文字的颜色产生影响，其他主题不受此属性影响。

或可以使用快速调用：
```
List<String> list = new ArrayList<>();
list.add("菜单1");
list.add("菜单2");
list.add("菜单3");
BottomMenu.show(me, list);
```

为底部对话框添加标题：
```
BottomMenu.show(me, list).setTitle("这里是标题测试");
```

### 自定义布局：
从 2.2.3 版本起支持 MessageDialog、SelectDialog、InputDialog和BottomMenu 的自定义布局，因为一些原因，选择 Material 风格时仅支持对话框全部使用自定义布局。

使用方法举例：
```
//初始化布局：
View customView = LayoutInflater.from(me).inflate(R.layout.layout_custom, null);
//启动对话框
MessageDialog.show(me, null, null, "知道了", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {

                    }
                }).setCustomView(customView);
```

## 附加功能：
在任何一种对话框中都可以使用.setCanCancel(boolean)来设置是否可以点击对话框以外的区域关闭对话框，提示类默认都是禁止的，选择、输入对话框默认也是禁止的，消息对话框默认是允许的。

使用方法可以参考以下代码：
```
WaitDialog.show(me, "载入中...").setCanCancel(true);
```

在空祖家的对话框组件中，您可以使用监听器来监听对话框的生命周期，Demo如下：
```
WaitDialog.show(me, "载入中...").setCanCancel(true).setDialogLifeCycleListener(new DialogLifeCycleListener() {
    @Override
    public void onCreate(AlertDialog alertDialog) {
        //此时对话框创建
    }
    @Override
    public void onShow(AlertDialog alertDialog) {
        //此时对话框显示
    }
    @Override
    public void onDismiss() {
        //此时对话框关闭
    }
});
```

另外提供一些定制属性：
```
DialogSettings.dialog_title_text_size = -1;                 //设置对话框标题文字大小，<=0不启用
DialogSettings.dialog_message_text_size = -1;               //设置对话框内容文字大小，<=0不启用
DialogSettings.dialog_button_text_size = -1;                //设置对话框按钮文字大小，<=0不启用
DialogSettings.dialog_menu_text_size = -1;                  //设置菜单默认字号，<=0不启用
DialogSettings.tip_text_size = -1;                          //设置提示框文字大小，<=0不启用
DialogSettings.ios_normal_button_color = -1;                //设置iOS风格默认按钮文字颜色，=-1不启用
DialogSettings.dialog_background_color = R.color.white;     //控制 TYPE_MATERIAL 和 TYPE_KONGZUE 两种风格时对话框的背景色，=-1时不启用
```

## 开源协议
```
Copyright Kongzue Dialog

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

 http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## 更新日志：
v2.2.9.4:
- 修复释放问题，提升健壮性；

v2.2.9.3:
- 修复bug；
- 兼容性更新；

v2.2.9:
- 不再支持v1版本对话框库；

v2.2.8:
- 修复了对话框生命周期 dialogLifeCycleListener 存在的问题；

v2.2.7:
- 暂时移除了 WaitDialog.dismiss(); 后的延迟，该延迟可能导致 WindowLeaked 异常，解决方案后续版本更新；
- 修复对话框生命周期监听器不会重置的问题，现在在启动一个新的对话框时监听器会重置；
- TipDialog 提供了 show(context, tip, type) 快速创建方法；

v2.2.6:
- DialogSettings 新增属性 DEBUGMODE 以决定框架是否打印 log 日志；
- InputDialog 在点击确定后自动关闭输入法；

v2.2.5:
- 优化执行流程，修复可能出现的死锁问题：
```
经测试，在 Dialog 显示的情况下，遇到 Activity 被 finish() 掉后导致出现问题：android.view.WindowLeaked
此问题导致接下来用户程序在未结束掉全部进程的情况下，再无法重新启动任何对话框
在 2.2.5 版本中我们将提供方法 DialogSettings.unloadAllDialog()，您可以在 Activity 的 onDestroy() 事件执行此方法来关闭所有在队列中的 Dialog。
```
- 新增 DialogSettings.dialog_background_color 可控制 TYPE_MATERIAL 和 TYPE_KONGZUE 两种风格时对话框的背景色。


v2.2.4:
- TipDialog 和 WaitDialog 现在可以支持更多文字的扩展了，且最大行数限定为3行；
- 调整白色界面时模糊不透明度 180 → 200；

v2.2.3:
- 修复bug；
- 新增添加自定义布局，目前支持 MessageDialog、SelectDialog、InputDialog和BottomMenu，因为一些原因，选择 Material 风格时仅支持对话框全部使用自定义布局。

v2.2.2:
- InputDialog 点击确定后默认不关闭对话框，可以作出判断后再使用 dialog.dismiss() 关闭；

v2.2.1:
- 修复多次重复调用 WaitDialog 和 TipDialog 时可能存在的叠加问题；
- 底部菜单 BottomMenu 现已全部拒绝使用margin\padding - Horizontal\Vertical以避免部分设备上的兼容问题导致的布局显示错误；
- 统一背景遮罩层 40% 不透明度；

v2.2.0:
- 修复bug；
- 底部菜单支持取消按钮文字设置；
- 底部菜单支持菜单字号设置（dialog_menu_text_size）；

v2.1.9:
- Android Support 支持库升级到 27.1.0；

v2.1.8:
- 修复显示标题的底部菜单情况下第一位菜单按下状态不符的bug；

v2.1.7:
- 优化iOS对话框消失时的动画，与最新版本的iOS保持一致；
- 底部菜单新增标题功能；

v2.1.6:
- 底部菜单iOS风格时的线条颜色优化；

v2.1.5:
- iOS风格对话框线条颜色优化；

v2.1.4:
- 底部菜单iOS风格时的透明度优化；

v2.1.3:
- WaitDialog和TipDialog现在可以衔接了；
- 优化iOS模式下对话框的透明度和模糊程度；

v2.1.2:
- Android Support 支持库升级到 26.1.0；

v2.1.1:
- iOS主题的对话框、等待框以及提示框、底部菜单增加即时模糊效果；

v2.1.0:
- 新增底部菜单（BottomMenu）;
- 新增iOS对话框出现、消失动画；
- 修复一些细节bug；

v2.0.9:
- 序列启动对话框；

v2.0.8:
- 修复bug；

v2.0.7:
- 修复bug；

v2.0.6:
- 修复bug；

v2.0.5:
- 新增通知消息在使用Kongzue主题时可自定义颜色；

v2.0.4:
- 提供消息与通知功能；

v2.0.3:
- 提供部分文字大小和颜色修改；

v2.0.2:
- 提供Light和Dark两种黑白主题模式；

v2.0.1:
- TipDialog提供自定义提示图标；
- WaitDialog可通过dismiss()方法关闭等待提示框；

v2.0.0:
- 新增v2组件库；
