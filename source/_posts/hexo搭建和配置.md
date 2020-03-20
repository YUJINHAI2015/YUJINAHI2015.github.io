
[官方网站](https://hexo.io/zh-cn/docs/)
### hexo安装流程
- 安装 [nodejs](https://nodejs.org/en/)

- 安装 [git](https://git-scm.com)

- 安装 hexo ` npm install -g hexo-cli `

### 运行网站
```
$ hexo init <folder>
$ cd <folder>
$ npm install

```
运行后的文件结构如下面所示：

{% asset_img file_struct.png file_struct %}

### _config.yml配置信息
[配置信息](https://hexo.io/zh-cn/docs/configuration)

### hexo创建文件（创建的.md文件就会直接显示到网站上面）
- ` hexo new <filename>` 
> 例如：`hexo new test` 该命令创建的文件会直接放在 _posts 文件夹下面，这里面的文件可以直接发布到网站上面。

- `hexo new drafts <filename> `
> 例如：`hexo new drafts my_draft` drafts 是 hexo 的关键字，所创建的文件会放到 _drafts 文件夹下面，需要通过 `hexo publish <filename>` 将文件放到 _posts 里面。

- `hexo new <folder> <filename>`
> 例如： `hexo new my_folder my_filename` 这种方式创建的文件，要通过拼接的方式，才能够访问到里面的文件。

- 资源文件 `post_asset_folder: true` 
> 每次 new 一个文件，就会创建相应的资源文件夹。
> 
> 如果只是少量的资源文件，可以自己放到 `source/images` 里面。

- 数据文件 `source/_data`
> 一些需要重复使用的文件，可以通过这种方式存储。

- 创建新的标签页 `hexo new page [name]`
>这种方式创建了一个二级页面

### hexo服务器
- 安装 `npm install hexo-server --save`

- 启动 `hexo server`

- 访问 `http://localhost:4000`

### hexo生成和部署
- 生成 `hexo g` 或 `hexo generate`

- 部署 `hexo d` 或 `hexo deploy`

### hexo发布到GitHub

1、新建 [git 仓库](https://github.com/YUJINHAI2015/yujinhai2015.github.io/settings) ，命名方式：`<你的 GitHub 用户名>.github.io`
> 例如：`https://github.com/YUJINHAI2015/yujinhai2015.github.io`

2、创建两条分支，`master` 和 `hexo`

> `master` 分支放网站生成文件，编译后的文件。也就是 `deploy` 的路径。
> 
> `hexo` 分支放网站的源文件。也就是 `hexo init` 后的文件。
> 
> __注意: .gitignore 文件中要包含 public 一行__

{% asset_img hexo_branch.png hexo_branch %}

3、将 [Travis CI](https://github.com/marketplace/travis-ci) 添加到你的 `GitHub` 账号中

4、前往 `GitHub` 的 [Applications settings](https://github.com/settings/installations)，配置 `Travis CI` 权限，使其能够访问你的 `repository`。

5、在 `GitHub` 中新建 [Personal Access Token](https://github.com/settings/tokens)，只勾选 `repo`选项，然后复制 `Token` 并保存好。

6、打开 [Travis CI](https://travis-ci.com)，按照步骤打开 `setting`

{% asset_img travis_setting.png travis_setting %}

7、找到 `Environment Variables` 在 `NAME` 添加 `github_token`, `VALUE` 添加从 `GitHub` 复制的 `token`, `DISPLAY VALUE IN BUILD LOG` 不打开。
> `github_token` 是自己规定的 `key` ，在后面会继续用到。

{% asset_img travis_add_token.png token %}

8、在你的 `Hexo` 站点文件夹中新建一个 `.travis.yml` 文件

{% asset_img file_struct.png file_struct %}

9、配置 `.travis.yml` 和 `_config.yml`
`.travis.yml` 能够实现自动部署
`_config.yml` 是 `hexo` 的配置文件
这里要特别注意yml的语法格式，一定要用空格键进行缩进，不能用Tab.

打开 `_config.yml` 文件，在 `deploy` 字段中修改为：

```
deploy:
  # 提交 Git 仓库
  type: git 
  # 分支是 master 这里放在编译后的文件
  branch: master 
  # repo 里面有个字段 github_token 是在Travis CI 里面添加token规定的。
  repo: https://github_token@github.com/YUJINHAI2015/yujinhai2015.github.io.git
  
```

打开 `.travis.yml`文件

```
language: node_js # 设置语言
sudo: required # 需要sudo权限
node_js: stable # 设置相应版本

# 指定缓存模块，可选。缓存可加快编译速度。
cache:
  directories:
    - node_modules

# 指定博客源码分支，因人而异。hexo博客源码托管在独立repo则不用设置此项
branches:
  only:
    - web

# tarvis生命周期执行顺序详见官网文档
before_install:
  - npm install -g hexo-cli
# Submodules
  # 这两步便是将作为 sub module 的主题下载下来
  - git submodule init
  - git submodule update

# Start: Build Lifecycle
install:
  - npm install
  - npm install hexo-deployer-git --save

script:
    - hexo clean # 清除
    - hexo generate # 生成


# 设置git提交名，邮箱；替换真实token到_config.yml文件，最后depoy部署
after_script:
  - git config user.name "yujinhai"
  - git config user.email "yujinhai2019@163.com"
  # 替换同目录下的_config.yml文件中gh_token字符串为travis后台刚才配置的变量，注意此处sed命令用了双引号。单引号无效！
  - sed -i "s/github_token/${github_token}/g" ./_config.yml
  - hexo deploy
# End: Build LifeCycle

```

10、配置 [next](https://github.com/iissnan/hexo-theme-next) 主题

- 先`fork next`主题，不然`TravisCI`会下载不下来

- `git submodule add https://github.com/你自己的仓库/hexo-theme-next.git themes/next` [submodule](https://www.jianshu.com/p/9000cd49822c)

- 更改`_config.yml`中的主题


