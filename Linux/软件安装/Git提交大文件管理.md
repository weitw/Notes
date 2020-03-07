### 1. 安装

> 注意：安装 Git LFS 需要 Git 的版本不低于 1.8.5，查看git版本：`git --version`

依次执行以下命令

- `curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash`

- `sudo apt-get install git-lfs`

### 2. 使用方法

- 执行 `git lfs install` ，这条命令每个仓库下只需要初次执行即可
- 使用 `git lfs track` 命令进行大文件追踪 例如`git lfs track "*.png"` 追踪所有后缀为png的文件
- 使用 `git lfs track` 查看现有的文件追踪模式
- 提交代码需要将`gitattributes`文件提交至仓库. 它保存了文件的追踪记录
- 提交后运行`git lfs ls-files` 可以显示当前跟踪的文件列表
- 将代码 push 到远程仓库后，LFS 跟踪的文件会以『Git LFS』的形式显示:
- clone 时 使用'git clone' 或 `git lfs clone`均可