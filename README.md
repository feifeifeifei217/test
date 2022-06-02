解决You've successfully authenticated, but GitHub does not provide shell access.

在git push 的时候提示输入账号密码。但我在另一个项目配置过 ssh 免密的。并且现在 git 也不允许 http 连接，所以提供账号密码也没办法 push。

$ git push -u origin main
Username for 'https://github.com': xx@qq.comxx
Password for 'https://xx@qq.com@github.com':
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see <https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/> for more information.
fatal: Authentication failed for 'https://github.com/balala8/N0va_for_mac.git/'

原因&解决
虽然是用 git 命令push，但本质上仍然是 https，所以不允许提交。
使用 git remote -v 查看现在的远程 url 地址。

git remote -v
origin <https://github.com/balala8/N0va_for_mac.git> (fetch)

origin <https://github.com/balala8/N0va_for_mac.git> (push)

使用下面的改 url 链接。

git remote set-url origin  git@github.com:balala8/N0va_for_mac.git
1
再次查看

git remote -v
origin git@github.com:balala8/N0va_for_mac.git (fetch)
origin git@github.com:balala8/N0va_for_mac.git (push)
已经改为 ssh 了。现在可以正常 push 了。

后续
使用ssh测试链接。

ssh git@github.com

会发现

You've successfully authenticated, but GitHub does not provide shell access.

这句话其实一直存在，它只是想告诉你，github 不允许 shell 交互。仅此而已。
