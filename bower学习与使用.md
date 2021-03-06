﻿#bower学习与使用#
---------

V0.0.2
@gitgump
2015/12/01



##什么是bower##
bower是一个客户端技术的软件包管理器，它可用于搜索、安装和卸载如JavaScript、HTML、CSS之类的网络资源。



##为什么使用bower##
1. 节省时间。为什么要学习bower的第一个原因，就是它会为你节省寻找客户端的依赖关系的时间。每次我需要安装jQuery的时候，我都需要去jQuery网站下载包或使用CDN版本。但是有了bower，你只需要输入一个命令，jquery就会安装在本地计算机上，你不需要去记版本号之类的东西，你也可以通过bower的info命令去查看任意库的信息。

2. 脱机工作。bower会在用户主目录下创建一个.bower的文件夹，这个文件夹会下载所有的资源、并安装一个软件包使它们可以离线使用。如果你熟悉Java，bower即是一个类似于现在流行的Maven构建系统的.m2仓库。每次你下载任何资源库都将被安装在两个文件夹中 —— 一个在的应用程序文件夹，另一个在用户主目录下的.bower文件夹。因此，下一次你需要这个仓库时，就会用那个用户主目录下.bower中的版本。

3. 可以很容易地展现客户端的依赖关系。你可以创建一个名为bower.json的文件，在这个文件里你可以指定所有客户端的依赖关系，任何时候你需要弄清楚你正在使用哪些库，你可以参考这个文件。

4. 让升级变得简单。假设某个库的新版本发布了一个重要的安全修补程序，为了安装新版本，你只需要运行一个命令，bower会自动更新所有有关新版本的依赖关系。



##安装bower##
bower的使用依赖于以下工具
1. node，下载最新版本的node.js
2. npm，npm是node程序管理包，它是捆绑在nodejs的安装程序上的，所以一旦你已经安装了node，npm也就安装好了。
3. git，用于从git仓库获取代码包

###Install：###
```
npm install –g bower
```
-g表示全局安装



##使用bower##
终端输入bower help可以看到bower提供的所有操作：
```
$ bower help
Usage:

    bower <command> [<args>] [<options>]

Usage:

    bower <command> [<args>] [<options>]
Commands:

    cache                   Manage bower cache
    help                    Display help information about Bower
    home                    Opens a package homepage into your favorite browser
    info                    Info of a particular package
    init                    Interactively create a bower.json file
    install                 Install a package locally
    link                    Symlink a package folder
    list                    List local packages - and possible updates
    login                   Authenticate with GitHub and store credentials
    lookup                  Look up a package URL by name
    prune                   Removes local extraneous packages
    register                Register a package
    search                  Search for a package by name
    update                  Update a local package
    uninstall               Remove a local package
    unregister              Remove a package from the registry
    version                 Bump a package version
Options:

    -f, --force             Makes various commands more forceful
    -j, --json              Output consumable JSON
    -l, --log-level         What level of logs to report
    -o, --offline           Do not hit the network
    -q, --quiet             Only output important information
    -s, --silent            Do not output anything, besides errors
    -V, --verbose           Makes output more verbose
    --allow-root            Allows running commands as root
    -v, --version           Output Bower version
    --no-color              Disable colors
See 'bower help <command>' for more information on a specific command.
```


###包的安装###
bower是一个软件包管理器，所以你可以在应用程序中用它来安装新的软件包。举例来看一下来如何使用bower安装JQuery，在你想要安装该包的地方创建一个新的文件夹，键入如下命令：
```
bower install jquery
```
####**--save-dev or --save?**####
1. 需要在工程中引用并且最终的产物需要包含的包，使用bower install packageName --save，这会将包添加到配置文件dependencies声明里，例如需要在html里引用的js文件；
2. 开发需要但是不会影响最终产物的包，使用bower install packageName --save-dev，这会将包添加到配置文件devDependencies声明里，例如与测试相关的工具；
3. 如果不添加任何参数则会安装在当前项目路径但是不会写入配置文件里；
4. bower install等效于bower install --save，执行这条命令会将配置文件里在dependencies声明的包下载下来；
5. bower install --save-dev，执行这条命令会将配置文件里在dependencies以及devDependencies声明的包全部下载下来。
6. bower以上的特性与npm的表现一致。

**Hint：注意默认使用git协议下载包，而内网屏蔽了git协议，如果下载不了可用以下命令行将协议改为https：**
```
git config --global url."https://".insteadOf "git://"
```
如果想换回来：
```
git config --global --unset url."https://".insteadOf
```

上述命令完成以后，你会在你刚才创建的目录下看到一个bower_components的文件夹，其中目录如下：
```
$ tree bower_components/
bower_components/
└── jquery
    ├── README.md
    ├── bower.json
    ├── component.json
    ├── composer.json
    ├── jquery-migrate.js
    ├── jquery-migrate.min.js
    ├── jquery.js
    ├── jquery.min.js
    ├── jquery.min.map
    └── package.json

1 directory, 10 files
```
可以通过编辑.bowerrc文件指定包安装的位置，如
```
{
  "directory": "www/lib"
}
```


###包的使用###
下载下来你想要应用的程序包之后，就可以像一般的库文件一样在html文件里加上引用连接：
```
<script type="text/javascript" src="bower_components/jquery/dist/jquery.min.js"></script>
```
就可以正常使用了。


###查看已安装包的列表###
如果你想找出所有安装在应用程序中的包，可以使用list命令：
```
$ bower list
bower check-new     Checking for new versions of the project dependencies...
HelloIonic /home/tianxud/tp/webapp/TPMiFi/ion
├── angular-local-storage#0.2.3
├─┬ angular-toastr#1.5.0
│ └── angular#1.4.3 (1.5.0-build.4380+sha.25f1bba available)
├─┬ angular-translate#2.8.1
│ └── angular#1.4.3 (1.4.7 available, latest is 1.5.0-build.4380+sha.25f1bba)
├─┬ angular-translate-loader-partial#2.8.1
│ └─┬ angular-translate#2.8.1
│   └── angular#1.4.3
├── cryptojslib#3.1.2
├─┬ ionic#1.1.0 (latest is 1.1.1)
│ ├── angular#1.4.3 (latest is 1.5.0-build.4380+sha.25f1bba)
│ ├─┬ angular-animate#1.4.3 (latest is 1.5.0-build.4380+sha.25f1bba)
│ │ └── angular#1.4.3
│ ├─┬ angular-sanitize#1.4.3 (latest is 1.5.0-build.4380+sha.25f1bba)
│ │ └── angular#1.4.3
│ └─┬ angular-ui-router#0.2.13 (latest is 0.2.15)
│   └── angular#1.4.3 (1.5.0-build.4380+sha.25f1bba available)
└─┬ oclazyload#1.0.8
  └── angular#1.4.3 (1.5.0-build.4380+sha.25f1bba available)
```


###搜索包###
```
$ bower search bootstrap
Search results:

bootstrap git://github.com/twbs/bootstrap.git
angular-bootstrap git://github.com/angular-ui/bootstrap-bower.git
sass-bootstrap git://github.com/jlong/sass-twitter-bootstrap.git
```


###查看安装包的信息###
```
$ bower info bootstrap
bower bootstrap#*           not-cached git://github.com/twbs/bootstrap.git#*
bower bootstrap#*              resolve git://github.com/twbs/bootstrap.git#*
bower bootstrap#*             download https://github.com/twbs/bootstrap/archive/v3.0.0.tar.gz
bower bootstrap#*              extract archive.tar.gz
bower bootstrap#*             resolved git://github.com/twbs/bootstrap.git#3.0.0

{
  name: 'bootstrap',
  version: '3.0.0',
  main: [
    './dist/js/bootstrap.js',
    './dist/css/bootstrap.css'
  ],
  ignore: [
    '**/.*'
  ],
  dependencies: {
    jquery: '>= 1.9.0'
  },
  homepage: 'https://github.com/twbs/bootstrap'
}

Available versions:
  - 3.0.0
  - 3.0.0-rc1
  - 3.0.0-rc.2
  - 2.3.2
 .....
```


###卸载包###
```
$ bower uninstall jquery
```


##bower.json##
bower.json文件的使用可以让包的安装更容易，你可以在应用程序的根目录下创建一个名为“bower.json”的文件，并定义它的依赖关系。使用bower init 命令来创建bower.json文件：
```
$ bower init
? name mifix
? description A webapp for mifi
? main file 
? what types of modules does this package expose? 
? keywords hybird
? authors Tian Xudong <tianxudong@tp-link.net>
? license MIT
? homepage https://github.com/GitGump
? set currently installed components as dependencies? Yes
? add commonly ignored files to ignore list? Yes
? would you like to mark this package as private which prevents it from being accidentally published to the registry? Yes

{
  name: 'mifix',
  homepage: 'https://github.com/GitGump',
  authors: [
    'Tian Xudong <tianxudong@tp-link.net>'
  ],
  description: 'A webapp for mifi',
  main: '',
  moduleType: [],
  keywords: [
    'hybird'
  ],
  license: 'MIT',
  private: true,
  ignore: [
    '**/.*',
    'node_modules',
    'bower_components',
    'test',
    'tests'
  ]
}

? Looks good? (Y/n)
```
生成的bower.json内容如下：
```
{
  "name": "mifix",
  "homepage": "https://github.com/GitGump",
  "authors": [
    "Tian Xudong <tianxudong@tp-link.net>"
  ],
  "description": "A webapp for mifi",
  "main": "",
  "moduleType": [],
  "keywords": [
    "hybird"
  ],
  "license": "MIT",
  "private": true,
  "ignore": [
    "**/.*",
    "node_modules",
    "bower_components",
    "test",
    "tests"
  ]
}
```



##参考资料：##
1.	http://segmentfault.com/a/1190000000349555
2.	https://github.com/bower/bower



