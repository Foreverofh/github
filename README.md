# github使用总结

标签（空格分隔）： github

---
##1.什么是github
- github是分散性版本管理系统,有助于多人协作开发的管理系统。


----------


##2.Git的导入

 - Git 属于分散型版本管理系统，是为版本管理而设计的软件。（svn是集中型版本管路系统）

###集中型和分散性的区别

- 集中型
    - 在服务器中创建一个仓库,将所有数据集中存放在服务器仓库当中,有便于管理的有点。开发人员在这个仓库中进行提交和更新.万一服务器丢失数据,永远也拿不到源代码。

![svn集中型管理系统][1]

- 分散性
    - 分散型拥有多个仓库，相对而言稍显复杂。不过，由于本地的开发环境中就有仓库，所以开发者不必连接远程仓库就可以进行开发。

![git分散型管理系统][2]


----------


- Git下载可以到官网去下载
- Git的初始化设置
 - 首先来设置使用 Git 时的姓名和邮箱地址。名字请用英文输入

 > `git config --global user.name '你的英文名字'`
   `git config --global user.email '你的邮箱'`


----------


- 提高命令输出的可读性

> `git config --global color.ur auto`


----------


##3.使用github的前期准备 (初次在 GitHub 建立仓库以及公开代码的流程)
- 注册github账号
- 设置自己头像
- 设置 SSH Key
  - GitHub 上连接已有仓库时的认证，是通过使用了 SSH 的公开密钥
认证方式进行的。现在让我们来创建公开密钥认证所需的 SSH Key，并
将其添加至 GitHub
  - 创建 SSH Key
  > `$ ssh-keygen -t rsa -C "your_email@example.com"`
  > Generating public/private rsa key pair.
    Enter file in which to save the key
    (/Users/your_user_directory/.ssh/id_rsa): 按回车键
    Enter passphrase (empty for no passphrase): 输入密码
    Enter same passphrase again: 再次输入密码

 - id_rsa 文件是私有密钥，id_rsa.pub 是公开密钥。

- 在github添加公钥 (在github->setting->SSH and GPG keys)
 - 添加完进行认证

 >  `$ ssh -T git@github.com`
 >The authenticity of host 'github.com (207.97.227.239)' can't be established.
RSA key fingerprint is fingerprint值 .
Are you sure you want to continue connecting (yes/no)? 输入yes

 - 如果验证成功,会出现以下字段
 
 ```Hi hirocastest! You've successfully authenticated, but GitHub does not provide shell access.```


----------


- 使用社区功能(Follow)
 -您所 Follow 的用户的活动就会显示在您的控制面板页面中。您可以通过这种方法知道那个人在 GitHub 上都做了些什么。


----------


- 在github **创建仓库** (new repository 按钮)
![创建仓库][3]
![仓库详细内容][4]
 - `Repository name`(仓库的名字)
 - `Description` (仓库的描述)
 - `Public`是公开的 Private私有的(每个月都要收费)
 - `Initialize this repository with a README` (如果本地项目是Git的项目就不需要勾选)
 - `Add .gitignore` 这个设定会帮我们把不需要在Git仓库中进行版本管理的文件记录在 .gitignore文件中，省去了每次根据框架进行设置的麻烦
 - `Add a license` 右侧的下拉菜单可以选择要添加的许可协议文件(一般选择MIT协议)
 - 连接仓库地址(https://github.com/用户名/项目名)
 - `README.md` 在初始化时已经生成好了。README.md 文件的内容会自动显示在仓库的首页当中


----------


- 公开代码
 - clone仓库地址
 `git clone 仓库地址`
 - 编写代码
  - 创建index.html,写上hello github
  - `git states` 查看仓库的状态
  - `git add index.html` , `git add` 命令将文件加入暂存区
  - `git commit -m'创建了index.html'`,  `git commit` 命令将文件加入保存区
  - `git commit -am "注释"` 对于 ***一个*** 文件操作（相当于`git add xxx` `git commit -m '注释'`）
  - `git log`命令查看提交日志
    - ```git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative``` 设置日志显示优化(`git lg`就可以查看日志信息)
 - `git push origin master` 把保存区的东西推送到github仓库上


----------


##4.通过实际操作选择Git
 - 基本操作
     -  **按住esc+按大写Z两次退出编辑器**
     - `git init` 初始化仓库
     - `git status` 查看仓库状态
     - `git add`——向暂存区中添加文件
     - `git commit -m'提交的注释'`——保存仓库的历史记录
     - `git log`——查看提交日志
     - `git log -p`显示文件的改动
     - `git diff`——查看更改前后的差别(查看当前工作树与暂存区的差别)
     > “+”号标出的是新添加的行，被删除的行则用“-”号标出
     - `git diff HEAD` 查看工作树和最新提交的差别


----------


 - 分支操作
    > 通过灵活运用分支，可以让多人同时高效地进行并行开发。在这里，我们将带大家学习与分支相关的 Git 操作

     -  `git branch`——显示分支一览表
     -  `git checkout xxx` ——切换分支xxx
     -  `git checkout -` ——切换上一级分支
     -  `git checkout  -b xxx`——创建、切换分支xxx
     -  `git merge xxx`——合并分支xxx
     >  **分支（feature）要 `git add ` 和 `git commit`
      我们假设 feature 已经实现完毕，想要将它合并到主干分支 master 中。首先切换到 master 分支，之后`git merge feature`**

     - git log  -- graph——以图表形式查看分支

     - 更改提交的操作
     -  git reset——回溯历史版本
     >  `git reset --hard fd0cbf0d4a25f747230694d95cac1be72d33441d`(哈希值可以在`git reflog`获取）
     -  `git reflog`命令，查看当前仓库的操作日志

         >  在日志中找出回溯历史之前的哈希值，通过 `git reset  --hard  哈希值`命令恢复到回溯历史前的状态。
            在日志中，我们可以看到 commit、checkout、reset、merge 等 Git 命令的执行记录
     - `git merge --no-ff fix-B` 消除冲突(合并的时候可能会有冲突)
     - 查看冲突部分并将其解决
     - 提交解决后的结果。
        > 冲突解决后，执行 git add命令与 git commit命令

    - ```git commit  -- amend```——修改提交信息（要修改上一条提交信息）
    - ```git rebase  - i```——压缩历史(**经常会使用**)
     > 在合并特性分支之前，如果发现已提交的内容中有些许拼写错误等，
    不妨提交一个修改，然后将这个修改包含到前一个提交之中，压缩成一
    个历史记录

    - `git rebase -i HEAD~2`（**重要**）
     > 用上述方式执行 git rebase命令，可以选定当前分支中包含
    HEAD（最新提交）在内的两个最新历史记录为对象，并在编辑器中
    打开（**比如我有一个历史管理记录提交代码有bug，之后修改正确提交代码。历史管理记录不需要错误的bug历史管理记录，所以要把这最新两条信息合并在一起，防止以后切换历史版本切换到bug版本**,）


----------

- 推送至远程仓库(**新建仓库千万别勾选READEM.md**)
  > Git 是分散型版本管理系统，但我们前面所学习的，都是针对单一本地仓库的操作。下面，我们将开始接触远在网络另一头的远程仓库。远程仓库顾名思义，是与我们本地仓库相对独立的另一个仓库。让我们先在 GitHub 上创建一个仓库，并将其设置为本地仓库的远程仓库。

 - git remote add——添加远程仓库

 > 在 GitHub 上创建的仓库路径为“git@github.com:用户名 /仓库名.git”。现在我们用 git remote add命令将它设置成本地仓库的远程仓库。 `git remote add origin git@github.com:用户名 /仓库名.git`

 - git push——推送至远程仓库
 >如果想将当前分支下本地仓库中的内容推送给远程仓库，需要用到
git push命令.`git push -u origin master`

 - 推送至 master 以外的分支
 > 除了 master 分支之外，远程仓库也可以创建其他分支

 - `git checkout -b feature-D`
 > 我们在本地仓库中创建了 feature-D 分支，现在将它 push `git push -u origin master` 给远程仓库并保持分支名称不变。现在，在远程仓库的 GitHub 页面就可以查看到 feature-D 分支了


----------


- 从远程仓库获取
 - `git clone`——获取远程仓库
 > 执行 git clone命令后我们会默认处于 master 分支下，同时系统
会自动将 origin 设置成该远程仓库的标识符。也就是说，当前本地仓库
的 master 分支与 GitHub 端远程仓库（origin）的 master 分支在内容上是
完全相同的

 - `git branch -a`
 > 我们用 git branch -a命令查看当前分支的相关信息。添加 -a 参数可以同时显示本地仓库和远程仓库的分支信息。
结果中显示了 remotes/origin/feature-D，证明我们的远程仓库中已经有了 feature-D 分支。
 - `git checkout -b feature-D origin/feature-D` 获取远程的 feature - D 分支
 > -b 参数的后面是本地仓库中新建分支的名称。为了便于理解，我们仍将其命名为 feature-D，让它与远程仓库的对应分支保持同名。新建分支名称后面是获取来源的分支名称。例子中指定了 origin/feature-D，就是说以名为 origin 的仓库（这里指 GitHub 端的仓库）的 feature-D 分支为来源，在本地仓库中创建 feature-D 分支。

 - 向本地的 feature - D 分支提交更改
 - `git commit -am "Add feature-D"`
 - `git push origin feature-D` 推送 feature - D 分支
 - `git pull`——获取最新的远程仓库分支
 - `git pull origin feature-D` 将本地的 feature-D 分支更新到最新状态。当前分支为 feature-D 分支。
 > 如果两人同时修改了同一部分的源代码，push时就很容易发生冲突。所以多名开发者在同一个分支中进行作业时，为减少冲突情况的发生，建议更频繁地进行 push 和 pull 操作.


















  [1]: http://a1.qpic.cn/psb?/V12ElRQM1w5HMI/1WYXzDPkravBdCD5n3vGMQ5LKGuqS.KGWETHSv1S0TI!/c/dGgBAAAAAAAA&ek=1&kp=1&pt=0&bo=TwKdAAAAAAADF.I!&tm=1488704400&sce=60-2-2&rf=0-0
  [2]: http://a1.qpic.cn/psb?/V12ElRQM1w5HMI/TQk5.WlXasgCpFLKVvEE3g*Ts2.bzpcN6TqakP*N5b8!/b/dGgBAAAAAAAA&bo=VwKVAQAAAAADB.M!&rf=viewer_4
  [3]: http://a1.qpic.cn/psb?/V12ElRQM1w5HMI/2XsmNKgdOrqKd7q6Ys35lSwlEA3WyyrcDY8sE0UjF8E!/b/dGgBAAAAAAAA&bo=lAE*AAAAAAADAI8!&rf=viewer_4
  [4]: http://a1.qpic.cn/psb?/V12ElRQM1w5HMI/SI1rB.GMdIb6VRy5xFmfuL6iG6jn5mNQ6Cj6SeshT30!/b/dGgBAAAAAAAA&bo=tQN.AgAAAAADAO8!&rf=viewer_4