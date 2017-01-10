# STRUTS2

###为什么要用它?
实现了一个 MVC 结构的 Web 框架:

* Action, 具体的处理 request 的部分 ===> Model
* Result, Action 返回的数据, 一般是 JSP 文件 ===> View
* FilterDispatcher, 用于过滤分发请求 ===> Controller

###优点:
* 使用简单集中的文件(struts.xml, web.xml, struts.properties)配置方法进行 Action 的调度, 配置修改都挺方便.
* 提供统一, 简单的表达式语言访问所有的可以访问的数据.
* 标准强大的 **验证框架** & **国际化框架**
* 强大的标签, 可以减少页面代码.
* 良好的 Ajax 支持.
* 简单的插件扩展.

----

###环境搭建:
* 去 [apache](http://archive.apache.org/) 下载全部包, 或者使用 Intelij的 Marven 管理添加依赖.
* 需要注意的是, lib 依赖需要是 project 级别的, lib 文件夹需要放在WEB-INFO/lib 下面
* 在 src 根目录添加 struts.properties, 进行struts 的全局配置
* 在 src 根目录添加 struts.xml, 进行Action 分发的配置

    ```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE struts PUBLIC
            "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
            "http://struts.apache.org/dtds/struts-2.0.dtd">
    <struts>
    
        <package name="default" namespace="/" extends="struts-default">
            <action name="hello" class="com.action.TestAction">
                <result>/success.jsp</result>
            </action>
        </package>
    
    </struts>
    ```
    
* 配置 WEB-INFO 目录下的 web.xml 文件, 添加 STRUTS 的过滤器:

    ```xml
   <filter>
       <filter-name>strut2</filter-name>
       <filter-class>
           org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter
       </filter-class>
   </filter>
    
   <filter-mapping>
       <filter-name>strut2</filter-name>
       <url-pattern>/*</url-pattern>
   </filter-mapping>
    
   <welcome-file-list>
       <welcome-file>index.jsp</welcome-file>
   </welcome-file-list>
    ```
* 建立 Java 包目录, 新建 Action 类, 继承ActionSupport 类.

    ```Java
    public class TestAction extends ActionSupport {
        //Action 属性
        private String hello;
    
        public String getHello() {
            return hello;
        }
    
        public void setHello(String hello) {
            this.hello = hello;
        }
    
        @Override
        public String execute() throws Exception {
            hello = "hello, world";
            //返回的是ActionSupport 中定义的几个常量
            return SUCCESS;
        }
    }
    ```


