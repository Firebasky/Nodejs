## npm

当我们没有项目的时候需要通过`npm -init`来部署一个项目

[使用“npm init”初始化项目](https://www.cnblogs.com/WD-NewDemo/p/11141384.html)

```
package name:                      你的项目名字叫啥
version:                          版本号
description:                       对项目的描述
entry point:                      项目的入口文件（一般你要用那个js文件作为node服务，就填写那个文件）
test command:                     项目启动的时候要用什么命令来执行脚本文件（默认为node app.js）
git repository:                    如果你要将项目上传到git中的话，那么就需要填写git的仓库地址（这里就不写地址了）
keywirds：                       项目关键字（我也不知道有啥用，所以我就不写了）
author:                         作者的名字（也就是你叫啥名字）
license:                        发行项目需要的证书（这里也就自己玩玩，就不写了）
```

[npm安装报错npm ERR! Refusing to install package with name "xxxx" under a packagexxxx](https://blog.csdn.net/controllerha/article/details/84256852)

### 解决方法

检查package.json下的name字段是不是项目名字和你安装的那个包名字相同了，如果一样就会报那个错，把项目名字改成和你安装不冲突的名字
