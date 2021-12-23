# 使用git提交代码到github时报错：Support for password authentication was removed on August 13, 2021.

使用git提交代码时报错如下：

remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
fatal: unable to access ‘https://github.com/xxx/xxx.git/’: The requested URL returned error: 403

如果以前是使用github账号密码提交代码的，从8月14号起将无法使用。
原因是github从8月14日起弃用了账密验证Git操作，将改用token或SSH密钥
需要改成token来代替密码
创建token的方法参照github的官方文档
https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token

创建完成后切记保存好生成的token，
然后在git push的时候，使用生成的token来代替密码就ok了
————————————————
版权声明：本文为CSDN博主「淋雨一直走..」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/mu_mu_mu_mu_mu/article/details/119712430