# 一. 项目中Git的一些操作

##  1. 鼠标右键 Git 选项含义：
    Git GUI Here：通过图形化的方式操作 git
    Git Bash Here：通过命令行操作 git（常用）

## 2. 用 SSH 方式操作 github
用ssh方式操作可以避免每次提交时都要输入账号密码
### (1) 生成 SSH key（公钥和私钥）
    ssh-keygen -t rsa -C "邮箱"
### (2) 配置公钥
    1. 在 C:/用户/当前用户/.ssh 找到 id_rsa.pub
    2. 复制 id_rsa.pub 中的信息
    3. 在 github 中 settings → SSH and GPG keys → New SSH key → ssh -T git @github.com
### (3) 复制 SSH 格式的链接
    code → SSH → Copied
### (4) 克隆项目
    在新建文件夹下右键选择Git Bash Here，并输入git clone + 刚刚复制的SSH格式的链接
### (5) 登录
    输入用户名：git config user.name "用户名"
    输入邮箱：git config user.email "邮箱"
    查看是否登陆成功：git config -l
    (出现用户名和邮箱表示登陆成功)
### (6) 拉取公司其他成员的提交
    拉取别人操作的信息： git pull 
### (7) 提交
    提交前需要先查看文件状态：git status
    添加自己修改的文件：git add 文件名
    （也可直接添加所有文件：git add .）
    提交到自己的 github：git commit -m"注释"
    查看自己做的操作：git log
    提交到公司服务器：git push
    （提交方法同用HTTP方式操作github中的提交方法，只不过不再需要输入账号密码了）
### (8) 错误提示
    ! [rejected] Info -> Info (non-fast-forward)
    error: failed to push some refs to 'github.com:Linchpin-L/yxhk-adm.git'
    hint: Updates were rejected because the tip of your current branch is behind
    hint: its remote counterpart. Integrate the remote changes (e.g.
    hint: 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
    是因为，没有及时更新自己的项目
    所以，一定要在其他成员提交之后及时更新自己本地的项目