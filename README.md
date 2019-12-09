"# try-make-package" 

## 学习开发composer包
- [转自](https://learnku.com/articles/6652/learn-to-develop-their-own-composer-package-and-to-use-packagist-github-updates)


- 使用
```bash
composer require getvkey/try-make-package dev-master
```

- 更新包
```bash
composer update getvkey/try-make-package
```

## composer命令
> composer list 显示所有命令

> composer show 显示所有包信息

- 如有 composer.lock 文件，直接安装，否则从 composer.json 安装最新扩展包和依赖；
> composer install

> composer create-project laravel/laravel Laravel –prefer-dist "5.1.*" 创建项目

> composer search packagename 搜索包

- composer update 的逻辑是按照 composer.json 指定的扩展包版本规则，把所有扩展包更新到最新版本，注意，是所有扩展包
- 如不确定请勿运行！
> composer update
- 从 composer.json 或者对应包的配置，并更新到最新；
```log
composer update vendor/package
composer update xxx/package 更新指定包
composer remove xxx/package 移除指定的包
```

- 添加安装 xxx/package, 可以指定版本，如： 
```log
composer require xxx/package
composer require xxx/package ~2.5
composer require xxx/package:2.5
composer require xxx/package=2.5
composer require xxx/package 2.5
```

- 下来介绍几个日常生产的流程，来方便加深大家的理解。

### 流程一：新项目流程 
```log
创建 composer.json，并添加依赖到的扩展包； 
运行 composer install，安装扩展包并生成 composer.lock； 
提交 composer.lock 到代码版本控制器中，如：git;
```

### 流程二：项目协作者安装现有项目 
- 克隆项目后，根目录下直接运行 composer install 从 composer.lock 中安装 指定版本 的扩展包以及其依赖；

> 此流程适用于生产环境代码的部署。

### 流程三：为项目添加新扩展包

- 使用 composer require vendor/package 添加扩展包； 
- 提交更新后的 composer.json 和 composer.lock 到代码版本控制器中，如：git;

```log
关于 composer.lock 文件
composer.lock 文件里保存着对每一个代码依赖的版本记录，提交到版本控制器中，并配合composer install 使用，保证了团队所有协作者开发环境、线上生产环境中运行的代码版本的一致性。
关于扩展包的安装方法
那么，准备添加一个扩展包，install, update, require 三个命令都可以用来安装扩展包，选择哪一个才是正确的呢？
答案是：使用 composer require 命令

另外，在手动修改 composer.json 添加扩展包后，composer update new/package 进行指定扩展包更新的方式，也可以正确的安装，不过不建议使用这种方法，因为，一旦你忘记敲定后面的扩展包名，就会进入万劫不复的状态，别给自己留坑呀。

上面的概念不论对新手或者老手来说，都比较混淆，主要记住这个概念：
原有项目新添加扩展的，都使用 composer require new/package 这种方式来安装。
需要加版本的话
composer require "foo/bar:1.0.0"

更新指定扩展到指定版本
有时候你之前使用过的扩展包，加入了新功能，你想更新单独这个扩展包到指定版本，也可以使用 require 来操作。
如下面例子，需要更新 “sami/sami”: “3.0.” 到 “sami/sami”: “3.2.”
```