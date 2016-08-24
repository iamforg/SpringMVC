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
访问localhost：8080/web-demo/login.do

request.getContextPath()     /web-demo
request.getServletPath()     /login.do
request.getRequestURI()      /web-demo/login.do


getFile/*         getFile可用
getFile/*/*       getFile/*可用
getFile/e*/*      getFile/e*可用
