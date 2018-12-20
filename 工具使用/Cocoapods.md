
#Cocopods安装

	$ ruby -v
	ruby 2.0.0p645 (2015-04-13 revision 50299) [universal.x86_64-darwin15]
	
	$ sudo gem update --system
	
	$ gem sources -l
	*** CURRENT SOURCES ***

	https://rubygems.org/

### pod setup更新卡住了怎么办

1. 在执行pod install命令时加上参数--verbose即:pod install 'ThirdPartyName' --verbose,可在终端详细显示安装信息，看到pod目前正在做什么\(其实是在安装第三方库的索引\)，确认是否是真的卡住。

2. 进入终端家目录，输入ls -a可看到隐藏的pod文件夹，输入cd .cocoapods进入pod文件夹，然后输入du -sh即可看到repos文件夹的容量，隔几秒执行一下该命令，可看到repos的容量在不断增大，待容量增大至300+M时，说明，repos文件夹索引目录已安装完毕。此时，pod功能即可正常使用。

3. 前往[https://github.com/CocoaPods/Specs，下载该索引，然后拷进repos文件夹，替换Specs，进入目录方法：](https://github.com/CocoaPods/Specs)

   ```
    cd ~/.cocoapods/repos  open ~/.cocoapods/repos
   ```

### Updating spec repo `master`\[!\] Failed to connect to GitHub to update the CocoaPods/Specs specs repo - Please check if you are offline, or that GitHub is down

[点击查看解决办法](https://stackoverflow.com/questions/38993527/cocoapods-failed-to-connect-to-github-to-update-the-cocoapods-specs-specs-repo)



4.更新cocoapods的源   https://www.aliyun.com/jiaocheng/357868.html



#Cocopods私有库


### 创建私有仓库（存放私有库）

1. open ~/.cocoapods/repos
1. pod repo add MyRepo xxx.xxx.git 私有仓库创建#先去git服务器创建一个私有仓库，然后绑定
1. pod repo list 列出本地仓库会发现本地多了一个新加仓库

### 创建私有库（一键搞定）


1. pod lib create MyTest
2. Podspec修改
3. pod lib lint [name].podspec 验证.podspec文件
5. git add  git commit私有库
6. pod spec lint [name].podspec 以验证在源代码存储位置和.podspec文件之间是否正确配置了所有内容
7. git tag 0.1.0 git push origin 0.1.0
8. echo "3.0" > .swift-version #指定swift版本
6. pod repo push MyRepo MyTest.podspec 提交索引
7. pod search pod updata

### 也可以自己创建各种配置文件

### 更新

1. 修改代码库

2. 需要在模块文件下找到.podspec文件并打开，找到s.version，修改版本号，大于当前版本并记住。

3. 命令行cd到Example文件下，通过cocoapods执行一遍pod update --no-repo-update

4. 提交代码 打标签 git tag 新版本。 git push origin --tags

5. pod repo push ImagineRepo TestPrivateLib.podspec --verbose --use-libraries --allow-warnings
6. pod repo push ImagineRepo PrivateLib.podspec --verbose --use-libraries --allow-warnings
7. pod repo push LazyPodspec LazyTool_iOS.podspec --verbose --use-libraries --allow-warnings
8. pod spec lint LazyTool_iOS.podspec --no-clean --verbose --allow-warnings
9. pod spec lint LazyTool_iOS.podspec --use-libraries --allow-warnings --verbose --no-clean
10. pod lib lint LazyTool_iOS.podspec --no-clean --verbose --allow-warnings --use-libraries 

pod lib lint LazyTool_iOS.podspec --verbose --fail-fast --allow-warnings --skip-import-validation --use-libraries --swift-version=3.3

### 常见问题

**1. pod search找不到**

rm ~/Library/Caches/CocoaPods/search_index.json

后在一次输入：pod search xxxx

**2. [!] The repo `MySpecs` at `../../../.cocoapods/repos/MySpecs` is not clean 错误**

解决：cd ~/.cocoapods/repos/MySpecs，git clean -f

**3. pod lib lint (检查本地pod)
[!] DemoPodSpecs did not pass validation, due to 2 warnings (but you can use --allow-warnings to ignore them).**
You can use the --no-clean option to inspect any issue.
解决办法：用 pod lib lint --allow-warnings 命令

**4. can't get podspec validation - ERROR | [iOS] xcodebuild: Returned an unsuccessful exit code**
[https://github.com/CocoaPods/CocoaPods/issues/4553](https://github.com/CocoaPods/CocoaPods/issues/4553)

**5. Pod静态框架依赖不能混合使用Swift和Objective-C**

[https://github.com/CocoaPods/CocoaPods/issues/7435](https://github.com/CocoaPods/CocoaPods/issues/7435)

[Cocoapods依赖问题](https://github.com/CocoaPods/CocoaPods/issues/3985)

['Pod Spec Lint'验证失败](https://github.com/CocoaPods/CocoaPods/issues/8125)

[Swift Static Libraries迁移实践](https://juejin.im/post/5be41956e51d4507e97302d2)

[OS中动/静态库支持bitcode的问题](https://juejin.im/post/5ab311c76fb9a028c42e18a9)

### test命令

1. pod repo push ImagineRepo TestPrivateLib.podspec --verbose --use-libraries --allow-warnings

2. cd ~/.cocoapods/repos/ImagineRepo  

### 参考链接
[官方链接](https://guides.cocoapods.org/making/private-cocoapods.html)

//公有
[创建你的第一个CocoaPod](https://code.tutsplus.com/tutorials/creating-your-first-cocoapod--cms-24332)

[使用私有Cocoapods仓库遇到的问题](https://www.jianshu.com/p/be0d77d959c6)

[制作自己的cocoapods](https://www.jianshu.com/p/c94d394f0be7)

[CocoaPods 私有仓库的创建（超详细）](https://www.jianshu.com/p/0c640821b36f)












