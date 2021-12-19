## Asp.net Core学习笔记

### ASP.NET Core 项目启动流程
1. csproj 文件中：targetframework指定目标框架。
2. ASP.NET Core 项目的入口：ASP.NET Core应用程序最初作为控制台应用程序启动，存在Main方法。
```C#
public class Program
    {
        public static void Main(string[] args)
        {
            CreateHostBuilder(args).Build().Run();
        }

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                });
    }
```
3. 进程内托管和进程外托管

---------------------------
Get是向服务器发索取数据的一种请求，而Post是向服务器提交数据的一种请求，在FORM（表单）中，Method默认为"GET"，实质上，GET和POST只是发送机制不同，并不是一个取一个发！

-------------------------
ORM: Object Relational Mapping, 对象关系映射

## 第4章　创建ASP.NET Core项目

## 第5章　ASP.NET Core项目启动流程

## 第7章　ASP.NET Core中的中间件及其工作原理

## 第8章　ASP.NET Core中的静态文件中间件

1. 应用程序请求处理管道没有可以提供静态文件所需的中间件——UseStaticFiles()中间件。
2. 为了提供默认页面，我们必须在应用程序的请求处理管道中插入UseDefaultFiles()中间件。
3. 注：必须在UseStaticFiles之前通过注册UseDefaultFiles来提供默认文件。UseDefaultFiles是一个URL重写器，实际上并没有提供文件。它只是将URL重写定位到默认文件，然后还是由静态文件中间件提供。地址栏中显示的URL仍然是根节点的URL，而不是重写的URL。
4. UseFileServer()中间件结合了UseStaticFiles()、UseDefaultFiles()和UseDirectory Browser()中间件的功能。