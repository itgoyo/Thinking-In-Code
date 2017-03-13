# Thinking-In-Code

### 当我老了，回想当年的自己是否真的问心无愧。

# Atom

### Mac环境下

![](http://p1.bqimg.com/567571/e60b820273c78809.png)

advanced-open-file

command+alt+o

打开资源文件

win->command

alt->option

command+shift+.

显示隐藏文件

ctrl+command+f

是否全屏显示软件

ctrl+command+a

截图

command+shift+p

command+alt+ESC

强制退出软件

导包（安装插件）

ctrl+shift+m

markdown预览


###代码单例

减少new创建的次数

```java

class EMPushHelper {

    private static EMPushHelper instance;

    public static EMPushHelper getInstance() {
        if(instance == null) {

            instance = new EMPushHelper();
        }

        return instance;
    }
```

### 线程池

管理已创建好的各个线程，不用每次开启线程都要长时间等待，以为开启线程是一个缓慢的过程

牺牲空间换时间
```java

public class ThreadUtils {

    private static Handler sHandler = new Handler(Looper.getMainLooper());

    private static Executor sExecutor = Executors.newSingleThreadExecutor();

    public static void runOnSubThread(Runnable runnable){
        sExecutor.execute(runnable);
    }

    public static void runOnMainThread(Runnable runnable){
        sHandler.post(runnable);

    }

}
```
### Toast单例

```java

public class ToastUtils {

    private static Toast sToast;

    public static void showToast(Context context, String msg){
        if (sToast==null){
            sToast = Toast.makeText(context.getApplicationContext(), msg, Toast.LENGTH_SHORT);
        }
        //如果这个Toast已经在显示了，那么这里会立即修改文本
        sToast.setText(msg);
        sToast.show();
    }
}
```

### 文字校验正则表达式

```java
public class StringUtils {

    public static boolean checkUsername(String username){
        if (TextUtils.isEmpty(username)){
            return false;
        }

        return username.matches("^[a-zA-Z]\\w{2,19}$");
    }

    public static  boolean checkPwd(String pwd){
        if (TextUtils.isEmpty(pwd)){
            return false;
        }
        return  pwd.matches("^[0-9]{3,20}$");
    }

    public static  String getInitial(String contact){
        if (TextUtils.isEmpty(contact)){
            return contact;
        }else {
            return contact.substring(0,1).toUpperCase();
        }
    }

}
```
### Android 6.0运行时权限
```java

        // 1. 动态申请权限

       if (ActivityCompat.checkSelfPermission(this, Manifest.permission.WRITE_EXTERNAL_STORAGE)!= PermissionChecker.PERMISSION_GRANTED){
           ActivityCompat.requestPermissions(this,new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},REQUEST_SDCARD);
           return;
       }

       showDialog("正在玩命登录中...");

       mLoginPresenter.login(username,pwd);
   }

   @Override
   public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
       super.onRequestPermissionsResult(requestCode, permissions, grantResults);
       if (requestCode==REQUEST_SDCARD){
           if (grantResults[0]==PermissionChecker.PERMISSION_GRANTED){
               //被授权了
               login();
           }else{
               showToast("没有给予该应用权限，不让你用了");
           }
       }
   }

   ```
