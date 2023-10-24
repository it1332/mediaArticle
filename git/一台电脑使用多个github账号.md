
# 一台电脑使用多个github账号

问题：同一台电脑上面多个项目并且项目对应的`github`账号不是同一个，但是你链接的时候默认走默认账户和默认的ssh配置。下面两种方法可以指定当前项目使用那个账号提交。

## 方法1: 使用SSH密钥

1. **配置SSH密钥：** 首先，确保你为每个GitHub账户生成了不同的SSH密钥对。这个网上一大堆生成ssh key和配置公钥的教程不懂的可以百度。

   ```bash
   # 为账户A生成SSH密钥
   ssh-keygen -t rsa -b 4096 -C "your.email@example.com"

   # 将SSH密钥添加到SSH代理
   ssh-add ~/.ssh/id_rsa_accountA

   # 在GitHub账户A的设置中添加SSH公钥（~/.ssh/id_rsa_accountA.pub）到SSH keys
   ```

   重复以上步骤为账户B生成另一个SSH密钥，并将其添加到GitHub账户B。

2. **配置SSH配置文件：** 创建或编辑`~/.ssh/config`文件，设置每个GitHub账户使用不同的密钥。如果.ssh文件下面没有`config`文件就新建一个`config`文件

   ```plaintext
   # 账户A的SSH配置
   # accountA 换成你的github用户名
   Host github.com-accountA
     HostName github.com
     User git
     IdentityFile ~/.ssh/id_rsa_accountA

   # 账户B的SSH配置
   # accountB 换成你的github用户名
   Host github.com-accountB
     HostName github.com
     User git
     IdentityFile ~/.ssh/id_rsa_accountB
   ```

   在本地的Git仓库目录下，将远程仓库的URL修改为使用上述配置中的Host：
   
   注意：`git@github.com-accountA` 默认连接没有`-github用户名` 自己加上去 **相当关键**

   ```bash
   git remote set-url origin git@github.com-accountA:username/repo.git # 对于账户A的项目
   git remote set-url origin git@github.com-accountB:username/repo.git # 对于账户B的项目
   ```

第一个方法使用 `ssh` 的方式就就完成了。

## 方法2: 使用Credential Helper （不推荐）

**注意这会清空默认的账号密码**

**注意这会清空默认的账号密码**

**注意这会清空默认的账号密码**

当你使用`https`协议提交的和拉取的时候，会使用默认账号和存储的默认用户名与密码（windows=>控制面板->所有控制面板项->凭据管理器->windows凭据下面可查看当前存储的账号密码）。

使用Git的Credential Helper可以确保在HTTP/HTTPS访问时使用指定的凭据。

1. **配置Credential Helper：**

   为账户A的项目配置Credential Helper：

   ```bash
   git config credential.helper 'store --file ~/.git-credentials-accountA'
   ```

   为账户B的项目配置Credential Helper：

   ```bash
   git config credential.helper 'store --file ~/.git-credentials-accountB'
   ```

   然后，在`~/.git-credentials-accountA`文件中存储账户A的凭据，在`~/.git-credentials-accountB`文件中存储账户B的凭据。

   ```plaintext
      protocol=https
      host=github.com
      username=your_username
      password=your_personal_access_token
   ```
   your_username替换为你的GitHub用户名，your_personal_access_token替换为你的GitHub Personal Access Token。Personal Access Token可以在GitHub的Settings -> Developer settings -> Personal access tokens中生成。


   清除全局凭据设置：确保没有全局凭据设置覆盖了项目级别的设置。在命令行中运行以下命令，清除全局凭据设置`git config --global --unset credential.helper` 注意这会清空默认的账号密码


请确保执行了以上步骤，并将每个项目的远程仓库URL设置为对应的SSH Host 或 Credential Helper 文件路径，这样Git就会使用正确的身份验证信息。如果问题依然存在，请确保你没有在其他地方进行了全局或者其他级别的覆盖配置。


+vx：**mock1332** 各平台IT课程一折起

**更多资源、文章请关注公众号：IT1332**

![更多资源、文章请关注公众号：IT1332](https://cdn.jsdelivr.net/gh/it1332/mediaArticleImages@main/wx-gzh/it1332_wx-login_b.png)