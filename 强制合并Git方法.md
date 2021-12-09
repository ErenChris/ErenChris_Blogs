git pull 强制覆盖本地的代码方式，下面是正确的方法：

git fatch --all

然后，你有两个选择：

1. git reset --hard origin/master

或者如果你在其他分支上：

2. git reset --hard origin/<other branch>

说明：

git fetch从远程下载最新的，而不尝试合并或rebase任何东西。

然后git reset将主分支重置为您刚刚获取的内容。 --hard选项更改工作树中的所有文件以匹配origin/master中的文件。
