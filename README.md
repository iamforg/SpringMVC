# SpringMVC
## 注解
#### @Deprecated注解的作用及传递性
注解的意思是：这个方法或雷不再建议使用，在新版本有其它方法或类可以代替这个使用，
以后也不会更新这个方法或类。

    @Deprecated
    public class parent{}
    public child extends parent{}
使用parent时系统会提示过时，但是使用它的子类不会收到这个提醒

## request中的path
| url-pattern | url     |getServletPath|getPathInfo|
| :------------- | :------------- | :------------- | :------------- |
|*.do        | localhost：8080/web-demo/login.do     |/login.do|null|
| /yj/*   |localhost:8080/demo-web/yj/getFile/we|/yj|/getFile/we|
| /     |localhost：8080/web-demo/getFile/ws|/getFile/ws|null|
|/*| localhost：8080/web-demo/getFile/ws       |为空字符串|/web-demo/getFile/ws |

```xml
url-pattern指web.xml中dispatcher的配置
<servlet-mapping>
  <servlet-name>dispatcher</servlet-name>
  <url-pattern>/yj/*</url-pattern>
</servlet-mapping>
```
```
一、
serlvet对url的过滤规则和顺序。当一个url传入servlet容器，servlet首先去掉当前应用上下文
路径，比如项目上下文路径是demo-web,url是localhost:8080/demo-web/getFile,
serlvet会将前面的去掉，剩下的/getFile去做映射匹配。这个映射匹配是有顺序的，当一个
servlet匹配成功后，不需再匹配其它servlet。
1.精准匹配，/getFile会直接匹配url-pattern是/getFile的servlet
2.最长路径匹配，如果一个servlet的url-pattern是/get*，另一个servlet的url-pattern是
/getF*容器会选择路径最长的getF*
3.扩展匹配，如果url最后包含扩展，容器会根据扩展匹配，如.do
4.如果上面3条都没匹配到，容器会根据url选择对应的资源；如果定义了defaultservlet，则容
器会丢给default servlet。

相对以filter，filter是一个链，一个url可以经过多个filter，顺序就是web.xml中定义
的顺序
二、
"/"开头，“/*”结尾的是路径匹配
"*."开头是扩展匹配
"/"是定义default servlet
其它是定义详细映射的。比如/getfile/show
定义”/*.action”这样一个看起来很正常的匹配会错,因为这个匹配即属于路径映射，也属于扩展映
射，导致容器无法判断。
```

```
当使用/yj/*作为url-pattern时，虽然可以访问到yj/login.do,但是css的访问路径变成
了/demo-web/yj/resources/css/login.css
```

# REST
