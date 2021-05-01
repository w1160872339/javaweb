https://www.kuangstudy.com/bbs/1386537787443974146

## 1、Tomcat

 服务器是一种被动的操作，用来处理用户的一些请求和给用户的一些响应信息。

**Tomcat**



Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为Tomcat 技术先进、性能稳定，而且**免费**，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个Java初学web的人来说，它是最佳的选择。

### 1.1、安装tomcat

tomcat官网：http://tomcat.apache.org/

![image-20210317224808395](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210317224808395.png)

### 1.2、tomcat启动

![image-20210317225113582](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210317225113582.png)

启动、关闭tomcat

![image-20210317225203904](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210317225203904.png)

可能遇到的问题：

1. Java环境变量没有配置
2. 乱码问题：配置文件中设置

### 1.3、tomcat配置

![image-20210317225435335](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210317225435335.png)

可以配置启动的端口号

- tomcat的默认端口号为：8080
- mysql：3306
- http：80
- https：443

```
<Connector port="8081" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```

可以配置主机名称host

```
<Host name="www.baidu.com"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
```

这种需要在本机配置域名映射

C:\Windows\System32\drivers\etc下的hosts文件

127.0.0.1 www.baidu.com

### 1.4、发布一个web网站

将自己的war包项目放到tomcat中webapps目录下，然后启动tomcat即可

网站应该有的结构

```
--webapps ：Tomcat服务器的web目录
    -ROOT
    -myblog ：网站的目录名
        - WEB-INF
            -classes : java程序
            -lib：web应用所依赖的jar包
            -web.xml ：网站配置文件
        - index.html 默认的首页
        - static 
            -css
                -style.css
            -js
            -img
         -.....
```

### 1.5、启动多个不同端口的Tomcat

在公司中，我们一个服务器需要启动多个项目，为了方便，不同项目访问只需要通过不同的端口号区分。

修改端口只需修改三处即可，以**tomcat8**为例

1、shutdown端口

![image-20210318113724868](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210318113724868.png)

2、HTTP端口

![image-20210318113738086](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210318113738086.png)

3、AJP端口

![image-20210318113750347](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210318113750347.png)

tomcat9版本不需要第三步了

注意：有时更新项目后不能得到及时刷新，这是可以清除缓存，进入tomcat目录下删除work文件夹里面的文件。

## 2、Http

### 2.1、什么是HTTP

HTTP（超文本传输协议）是一个简单的请求-响应协议，它通常运行在TCP之上。

- 文本：html，字符串，~ ….
- 超文本：图片，音乐，视频，定位，地图…….
- 80

Https：安全的

- 443

### 2.2、两个时代

- http1.0
  - HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源，断开连接（短连接）。
- http2.0
  - HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源（长连接）。‘

### 2.3、Http请求

- 客户端—-发请求—-服务端

百度：

```
Request URL: https://www.baidu.com/  请求地址
Request Method: GET    //请求方式get/post
Status Code: 200 OK    //状态码
Remote Address: 14.215.177.38:443  //远程ip地址
```

请求头

```
Accept:text/html  //支持的数据类型
Accept-Encoding:gzip, deflate, br  //支持的编码格式
Accept-Language:zh-CN,zh;q=0.9    //语言
Cache-Control:max-age=0  //缓存控制
Connection:keep-alive  //是否长连接
```

### 2.4、Http响应

- 服务端—-响应—-客户端

```
Cache-Control:private    缓存控制
Connection:Keep-Alive    连接
Content-Encoding:gzip    编码
Content-Type:text/html   类型
```

#### 1、响应体

```
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
Refresh：告诉客户端，多久刷新一次；
Location：让网页重新定位；
```

#### 2、响应状态码

200：请求响应成功 200

3xx：请求重定向

- 重定向：你重新到我给你新位置去；

4xx：找不到资源 404

- 资源不存在；

5xx：服务器代码错误 500 502:网关错误

问题：当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？

## 3、Servlet

### 3.1、Servlet简介

- Servlet就是sun公司开发动态web的一门技术
- Sun在这些API中提供一个接口叫做：Servlet，如果你想开发一个Servlet程序，只需要完成两个小步骤：
  - 编写一个类，实现Servlet接口
  - 把开发好的Java类部署到web服务器中。

**把实现了Servlet接口的Java程序叫做，Servlet**

### 3.2、HelloServlet

![image-20210318162918401](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210318162918401.png)

- 导入依赖

```
<!--添加Servlet和JSP依赖-->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
</dependency>
```

- 编写servlet类继承HttpServlet

```
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        ServletOutputStream outputStream = resp.getOutputStream();
        System.out.println("进入了doGet");
        //设置编码，防止中文乱码，默认是ISO-8859-1
        resp.setContentType("text/html"); //ajax异步请求为application/json格式
        resp.setCharacterEncoding("utf-8");
        PrintWriter out = resp.getWriter(); //响应流
        out.print("wa servlet2乱码测试");
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

- 配置映射

一、xml方式

```
<!--映射配置-->
  <servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.bug.servlet.HelloServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
  </servlet-mapping>
```

二、注解方式

```
@WebServlet("/hi")
public class HelloServlet extends HttpServlet {
```

- 配置tomcat
- 启动项目，访问路径

### 3.3、Servlet原理

Servlet是由Web服务器调用，web服务器在收到浏览器请求之后，会：

![image-20210318220210550](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210318220210550.png)

### 3.4、Mapping问题

1、一个Servlet可以指定一个映射路径

```
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
```

2、一个Servlet可以指定多个映射路径

```
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello2</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello3</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello4</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello5</url-pattern>
    </servlet-mapping>
```

3、一个Servlet可以指定通用映射路径

```
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello/*</url-pattern>
    </servlet-mapping>
```

4、默认请求路径

```
    <!--默认请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
```

5、指定一些后缀或者前缀等等….

```
<!--可以自定义后缀实现请求映射
    注意点，*前面不能加项目映射的路径
    hello/sajdlkajda.qinjiang
    -->
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>*.qinjiang</url-pattern>
</servlet-mapping>
```

6、优先级问题
指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求（404）；

```
<!--404-->
<servlet>
    <servlet-name>error</servlet-name>
    <servlet-class>com.kuang.servlet.ErrorServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>error</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```

### 3.5、ServletContext

 web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContext对象，它代表了当前的web应用

#### 1、共享数据

```xml
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//            this.getServletConfig()
//            this.getServletInfo()
//            this.getServletName()
        ServletContext servletContext = this.getServletContext();
        servletContext.setAttribute("name","潘儿子");
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req, resp);
    }
}
```

```xml
@WebServlet("/get")
public class GetServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();
        String name = (String) servletContext.getAttribute("name");
        //乱码
        resp.setContentType("text/html;charset=utf-8");
        resp.getWriter().print(name);
    }
}
```



必须先访问hello接口，然后访问get接口，才能获取name的值。

#### 2、获取初始化参数

web.xml中配置

```
    <!--配置一些web应用初始化参数-->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>
    
```

```xml
@WebServlet("/demo1")
public class DemoServlet01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = getServletContext();
        String url = servletContext.getInitParameter("url");
        resp.getWriter().print(url);
    }
}
```



#### 3、请求转发

```
@WebServlet("/demo2")
public class DemoServlet02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = getServletContext();
        //请求转发
        servletContext.getRequestDispatcher("/demo1").forward(req, resp);
//        RequestDispatcher requestDispatcher = req.getRequestDispatcher("/demo1");
//        requestDispatcher.forward(req,resp);
    }
}
```

#### 4、读取资源文件

编写b.properties文件

![image-20210320004726070](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210320004726070.png)

```
@WebServlet("/demo3")
public class DemoServlet03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/com/bug/servlet/b.properties");
        Properties properties = new Properties();
        properties.load(is);
        String user = properties.getProperty("username");
        String pwd = properties.getProperty("password");
        resp.getWriter().print("user:" + user +"\n" + "password:" + pwd);
    }
}
```

### 3.6、HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的一个HttpServletResponse；

- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

#### 1、简单分类

负责向浏览器发送数据的方法

```
ServletOutputStream getOutputStream() throws IOException;
PrintWriter getWriter() throws IOException;
```

负责向浏览器发送响应头的方法

```
    void setCharacterEncoding(String var1);
    void setContentLength(int var1);
    void setContentLengthLong(long var1);
    void setContentType(String var1);
    void setDateHeader(String var1, long var2);
    void addDateHeader(String var1, long var2);
    void setHeader(String var1, String var2);
    void addHeader(String var1, String var2);
    void setIntHeader(String var1, int var2);
    void addIntHeader(String var1, int var2);
```

响应的状态码

```
    int SC_CONTINUE = 100;
    int SC_SWITCHING_PROTOCOLS = 101;
    int SC_OK = 200;
    int SC_CREATED = 201;
    int SC_ACCEPTED = 202;
    int SC_NON_AUTHORITATIVE_INFORMATION = 203;
    int SC_NO_CONTENT = 204;
    int SC_RESET_CONTENT = 205;
    int SC_PARTIAL_CONTENT = 206;
    int SC_MULTIPLE_CHOICES = 300;
    int SC_MOVED_PERMANENTLY = 301;
    int SC_MOVED_TEMPORARILY = 302;
    int SC_FOUND = 302;
    int SC_SEE_OTHER = 303;
    int SC_NOT_MODIFIED = 304;
    int SC_USE_PROXY = 305;
    int SC_TEMPORARY_REDIRECT = 307;
    int SC_BAD_REQUEST = 400;
    int SC_UNAUTHORIZED = 401;
    int SC_PAYMENT_REQUIRED = 402;
    int SC_FORBIDDEN = 403;
    int SC_NOT_FOUND = 404;
    int SC_METHOD_NOT_ALLOWED = 405;
    int SC_NOT_ACCEPTABLE = 406;
    int SC_PROXY_AUTHENTICATION_REQUIRED = 407;
    int SC_REQUEST_TIMEOUT = 408;
    int SC_CONFLICT = 409;
    int SC_GONE = 410;
    int SC_LENGTH_REQUIRED = 411;
    int SC_PRECONDITION_FAILED = 412;
    int SC_REQUEST_ENTITY_TOO_LARGE = 413;
    int SC_REQUEST_URI_TOO_LONG = 414;
    int SC_UNSUPPORTED_MEDIA_TYPE = 415;
    int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
    int SC_EXPECTATION_FAILED = 417;
    int SC_INTERNAL_SERVER_ERROR = 500;
    int SC_NOT_IMPLEMENTED = 501;
    int SC_BAD_GATEWAY = 502;
    int SC_SERVICE_UNAVAILABLE = 503;
    int SC_GATEWAY_TIMEOUT = 504;
    int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

#### 2、下载文件

1. 要获取下载文件的路径
2. 下载的文件名是啥？
3. 设置想办法让浏览器能够支持下载我们需要的东西
4. 获取下载文件的输入流
5. 创建缓冲区
6. 获取OutputStream对象
7. 将FileOutputStream流写入到buffer缓冲区
8. 使用OutputStream将缓冲区中的数据输出到客户端！

```
@WebServlet("/file")
public class FileServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取下载文件的路径
        String realPath = this.getServletContext().getRealPath("/WEB-INF/classes/a.png");// '/'表示web根目录
        System.out.println("下载的文件路径：" + realPath);
        //2.获取要下载的文件名
        String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
        //3.设置想办法让浏览器能够支持(Content-Disposition)下载我们需要的东西,中文文件名URLEncoder.encode编码，否则有可能乱码
        resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(fileName,"UTF-8"));
        //4.获取下载文件的输入流
        FileInputStream in = new FileInputStream(new File(realPath));
        //5.创建缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];
        //6.获取OutputStream对象
        ServletOutputStream out = resp.getOutputStream();
        //7. 将FileOutputStream流写入到buffer缓冲区,使用OutputStream将缓冲区中的数据输出到客户端！
        while ((len=in.read(buffer)) != -1) {
            out.write(buffer,0,len);
        }
        in.close();
        out.close();
    }
}
```

#### 3、验证码功能

- 前端实现
- 后端实现，需要用到Java的图片类，生产一个图片

```
@WebServlet("/img")
public class ImageServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //如何让浏览器3秒自动刷新一次;
        resp.setHeader("refresh","3");
        //在内存中创建一个图片
        BufferedImage image = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
        //得到图片
        Graphics2D g = (Graphics2D) image.getGraphics(); //笔
        //设置图片的背景颜色
        g.setColor(Color.white);
        g.fillRect(0,0,80,20);
        //给图片写数据
        g.setColor(Color.BLUE);
        g.setFont(new Font(null,Font.BOLD,20));
        g.drawString(makeNum(),0,20);
        //告诉浏览器，这个请求用图片的方式打开
        resp.setContentType("image/jpeg");
        //网站存在缓存，不让浏览器缓存
        resp.setDateHeader("expires",-1);
        resp.setHeader("Cache-Control","no-cache");
        resp.setHeader("Pragma","no-cache");
        //把图片写给浏览器
        ImageIO.write(image,"jpg", resp.getOutputStream());
    }
    //生成随机数
    private String makeNum(){
        Random random = new Random();
        String num = random.nextInt(9999999) + "";
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < 7-num.length() ; i++) {
            sb.append("0");
        }
        num = sb.toString() + num;
        return num;
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

#### 4、实现重定向

![image-20210320172123691](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210320172123691.png)

B一个web资源收到客户端A请求后，B会通知A去访问另外一个web资源C，这个过程叫重定向。

常见场景：

- 用户登录

重定向和转发的区别？

- 请求转发url不会产生变化，重定向会发生变化
- 请求转发可以携带参数，重定向不能携带参数
- 请求转发只能发送一个请求，重定向至少发送两次请求

#### 5、简单实现登录重定向

```xml
<%--这里提交的路径，需要寻找到项目的路径--%>
<%--${pageContext.request.contextPath}代表当前的项目--%>
<form action="${pageContext.request.contextPath}/login" method="get">
    用户名：<input type="text" name="username"> <br>
    密码：<input type="password" name="password"> <br>
    <input type="submit">
</form>
```

```xml
  @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //处理请求
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println(username+":"+password);
        //重定向时候一定要注意，路径问题，否则404；
        resp.sendRedirect("/r/success.jsp");
    }
```

```java
  <servlet>
    <servlet-name>requset</servlet-name>
    <servlet-class>com.kuang.servlet.RequestTest</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>requset</servlet-name>
    <url-pattern>/login</url-pattern>
  </servlet-mapping>
```



```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>Success</h1>
</body>
</html>
```



### 3.7、HttpServletRequest

HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，HTTP请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest的方法，获得客户端的所有信息；

```
@WebServlet("/req")
public class ReqServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("url路径："+req.getRequestURL());
        System.out.println("uri路径："+req.getRequestURI());
        System.out.println("context路径："+req.getContextPath());
        req.getRequestDispatcher("/file").forward(req,resp);
    }
}
```

![image-20210320180403649](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210320180403649.png)

## 4、Cookie、Session

### 4.1、会话

**会话**：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话；

**有状态会话**：一个同学来过教室，下次再来教室，我们会知道这个同学，曾经来过，称之为有状态会话；

### 4.2、保存会话的两种技术

**cookie**

- 客户端技术（响应、请求）

**session**

- 服务器技术，利用这个技术，可以保存用户的会话信息？ 我们可以把信息或者数据放在Session中！

### 4.3、Cookie

**cookie：一般会保存在本地的 用户目录下 appdata；**

一个网站cookie是否存在上限！**聊聊细节问题**

- 一个Cookie只能保存一个信息；
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie；
- Cookie大小有限制4kb；
- 300个cookie浏览器上限

**删除Cookie；**

- 不设置有效期，关闭浏览器，自动失效；（默认）
- 设置有效期时间为 0 ；

**注意**

- cookie默认有效期是在浏览器关闭后失效，如果设置了有效期就在过期后失效

```
@WebServlet("/c2")
public class CookieDemo extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        //从客户端获取cookies
        Cookie[] cookies = req.getCookies();
        PrintWriter out = resp.getWriter();
        if (cookies != null) {
            boolean isFirst = true;
            for (int i = 0; i < cookies.length; i++) {
                if ("date".equals(cookies[i].getName())) {
                    isFirst = false; //不是第一次访问
                    String value = cookies[i].getValue();
                    long lastLoginTime = Long.parseLong(value);
                    Date date = new Date(lastLoginTime);
                    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss ");
                    String format = sdf.format(date);
                    out.print("你上一次访问的时间是：" + format);
                }
            }
            if (isFirst) {
                out.print("这是你第一次访问！");
            }
        }else {
            out.print("cookies为空！");
        }
        //设置cookie值
        Cookie cookie = new Cookie("date",System.currentTimeMillis()+"");
        cookie.setMaxAge(0);
        resp.addCookie(cookie);
    }
```

编码与解码，防止乱码

```
@WebServlet("/c3")
public class CookieDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        PrintWriter out = resp.getWriter();
        for (Cookie cookie : req.getCookies()) {
            if (cookie.getName().equals("name")) {
                out.write(URLDecoder.decode(cookie.getValue(),"utf-8") );
            }
        }
        Cookie cookie = new Cookie("name", URLEncoder.encode("筱语","utf-8"));
        resp.addCookie(cookie);
    }
}
```

### 4.3、Session（重点）

什么是session

- 服务器会给每一个用户（浏览器）创建一个session对象
- 一个session独占一个浏览器，主要浏览器没有关闭，这个session就存在
- 用户登录后，整个网站它都可以房屋——>保存用户的信息，保存购物车的信息。

![image-20210323084508377](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210323084508377.png)

- 给session中存用户信息

```
@WebServlet("/s1")
public class Session01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        //获取session
        HttpSession session = req.getSession();
        //设置值
        session.setAttribute("name", "筱语");
        //获取session的id
        String id = session.getId();
        if (session.isNew()) {
            resp.getWriter().write("session创建成功！id=" + id);
        } else {
            resp.getWriter().write("session已经存在了，id=" + id);
        }
        resp.getWriter().write(session.getAttribute("name").toString());
    }
}
```

- 获取session中存储的用户信息

```
@WebServlet("/s2")
public class Session02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        //获取session
        HttpSession session = req.getSession();
        //获取session的id
        resp.getWriter().write(session.getAttribute("name").toString());
    }
}
```

每次新打开一个浏览器访问地址，都会新建一个session会话，也会向客户端存储一个值为sessionId的cookie。

- 手动注销session

```
@WebServlet("/s2")
public class Session03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        //获取session
        HttpSession session = req.getSession();
        session.removeAttribute("name");
        //手动注销Session
        session.invalidate();
    }
}
```

- 设置session的失效时间，在web.xml中

```
  <!--设置Session默认的失效时间-->
  <session-config>
    <!--15分钟后Session自动失效，以分钟为单位-->
    <session-timeout>15</session-timeout>
  </session-config>
```

#### 7天免登录案例实现

思路：session在一次会话后就会结束，所以可以通过servletContext来存储当前的session，以sessionId为key，session对象为值，然后将sessionId存在客户端的cookie中，每次获取用户信息先去cookie中查找是否有这个id，然后通过该id获取servletContext中的session对象实现。

- 登录接口，将session存到ServletContext中

```
@WebServlet("/ss1")
public class SessionAn extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        HttpSession session = req.getSession();
        session.setAttribute("name","小腿");
        String sessionId = session.getId();
        Cookie cookie = new Cookie("session",sessionId);
        cookie.setMaxAge(Integer.MAX_VALUE);
        resp.addCookie(cookie);
        //存session对象
        this.getServletContext().setAttribute(sessionId,session);
        resp.getWriter().write("登录成功！");
    }
}
```

- 获取用户信息接口

```
@WebServlet("/ss2")
public class SessionAn2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        String sId = "";
        for (Cookie cookie : req.getCookies()) {
            if (cookie.getName().equals("session")) {
                sId = cookie.getValue();
            }
        }
        HttpSession session = (HttpSession) this.getServletContext().getAttribute(sId);
        String  name = (String)session.getAttribute("name");
        resp.getWriter().write("欢迎你，"+name);
    }
}
```

先访问ss1接口，设置用户信息到session中，然后访问ss2接口就可以拿到用户信息了。将cookie过期时间设置为7天即可。当关闭浏览器后，下次直接访问ss2接口就能拿到用户信息，相当于不用再通过ss1接口登录了。

注意：每次访问网站都会生成一个JsessionId在cookie中，而且会是不同的值。

### 4.4、session与cookie异同

| cookie                           | session                |
| -------------------------------- | ---------------------- |
| 存在客户端中，不安全             | 存在服务端中，比较安全 |
| 只支持存字符串数据               | 支持任意数据类型       |
| 单个cookie存的数据大小不能超过4k | 可存储数据远高于Cookie |

## 5、Filter（重点）

Filter：过滤器 ，用来过滤网站的数据；

- 处理中文乱码
- 登录验证…

![image-20210325121124401](https://gitee.com/xiaoyu-98/blogImage/raw/master/img/image-20210325121124401.png)

```
public class CharecterFilter  implements Filter {
    /**
     * web服务器启动执行该方法
     */
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("filter初始化了...");
    }
    /**
     * 1. 过滤中的所有代码，在过滤特定请求的时候都会执行
     * 2. 必须要让过滤器继续同行
     * @param req
     * @param resp
     * @param chain
     * @throws IOException
     * @throws ServletException
     */
    @Override
    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws IOException, ServletException {
        resp.setContentType("text/html;charset=utf-8");
        System.out.println("filter执行前...");
        chain.doFilter(req,resp); //放行，如果不写，程序会被拦截
        System.out.println("filter执行后...");
    }
    //web服务器关闭，执行方法
    @Override
    public void destroy() {
        System.out.println("filter销毁了...");
    }
}
```

在web.xml中配置Filter映射

```
<filter>
  <filter-name>CharecterFilter</filter-name>
  <filter-class>com.bug.filter.CharecterFilter</filter-class>
</filter>
<filter-mapping>
  <filter-name>CharecterFilter</filter-name>
  <url-pattern>/servlet/*</url-pattern>
</filter-mapping>
```

只会拦截/servlet路径的接口

定义Servlet类

```
public class ShowServlet extends HttpServlet {
    /**
     * 第一次访问servlet执行
     */
    @Override
    public void init() throws ServletException {
        System.out.println("servlet初始化init...");
    }
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("你好，filter...");
    }
    /**
     * 关闭tomcat执行
     */
    @Override
    public void destroy() {
        System.out.println("servlet销毁destroy执行...");
    }
}
```

在web.xml定义servlet的接口

```
  <servlet>
    <servlet-name>showServlet</servlet-name>
    <servlet-class>com.bug.servlet.ShowServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>showServlet</servlet-name>
    <url-pattern>/servlet/show</url-pattern>
  </servlet-mapping>
  <servlet-mapping>
    <servlet-name>showServlet</servlet-name>
    <url-pattern>/show</url-pattern>
  </servlet-mapping>
```

这里设置了两个路径给同一个servlet来测试filter的作用，由于filter只会过滤/serlvet的路径，所以访问/show时乱码问题不会解决。

## 6、监听器

监测网站在线人数（基于session）

1、编写一个监听器，实现HttpSessionListener

```
public class OnlineListen implements HttpSessionListener {
    /**
     * 监听session新创建时执行的方法
     * @param se
     */
    @Override
    public void sessionCreated(HttpSessionEvent se) {
        ServletContext sc = se.getSession().getServletContext();
        System.out.println("sessionId:" + se.getSession().getId());
        Integer onlineCount = (Integer) sc.getAttribute("onlineCount");
        if (onlineCount == null) {
            onlineCount = 1;
        } else {
            onlineCount++;
        }
        sc.setAttribute("onlineCount",onlineCount);
    }
    /**
     * 监听session销毁时执行方法
     * @param se
     */
    @Override
    public void sessionDestroyed(HttpSessionEvent se) {
        ServletContext sc = se.getSession().getServletContext();
        Integer onlineCount = (Integer) sc.getAttribute("onlineCount");
        if (onlineCount == null) {
            onlineCount = 0;
        } else {
            onlineCount--;
        }
        System.out.println("销毁session了--监听到");
        sc.setAttribute("onlineCount",onlineCount);
    }
}
```

2、web.xml中注册监听器

```
<!--监听器-->
<listener>
  <listener-class>com.bug.listener.OnlineListen</listener-class>
</listener>
```

session销毁方法

- 手动销毁 getSession().invalidate();

- 自动销毁 在web.xml中设置超时时间

  ```
   <session-config>
      <session-timeout>1</session-timeout>
    </session-config>
  ```

