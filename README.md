# Thinking-In-Code

### 当我老了，回想当年的自己是否真的问心无愧。

# Atom

### Mac环境下

![](http://p1.bqimg.com/567571/e60b820273c78809.png)

win->command

alt->option


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
