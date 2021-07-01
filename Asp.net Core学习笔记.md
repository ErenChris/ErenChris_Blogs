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