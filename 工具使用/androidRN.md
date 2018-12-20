# 安卓





# Mac安装SDKMAN
### 1. 下载
从官方网站下载SDKMAN
curl -s "https://get.sdkman.io" | bash

### 2. 配置
	执行环境变量配置脚本
	source "$HOME/.sdkman/bin/sdkman-init.sh"


### 3. 检查
	输入下面命令查看SDKMAN版本信息，以确保SDKMAN安装成功
	sdk version

正常情况会返回SDKMAN的版本信息

	SDKMAN 5.6.0+287

### 4. 写入.bash_profile
将下面内容写入.bash_profile最后以确保每次打开新的终端都可以直接使用sdk命令

	THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
	[[ -s "/Users/你的用户名/.sdkman/bin/sdkman-init.sh" ]] && source "/
	Users/你的用户名/.sdkman/bin/sdkman-init.sh"
	
	
### 5.切换环境
	首先安装SDKMAN：https：//sdkman.io/install 然后......

	使用以下命令安装Oracle JDK 8： sdk install java 8.0.181-oracle
	安装OpenJDK 11： sdk install java 11.0.0-open
	换成：
	
	切换到JDK 8 sdk use java 8.0.181-oracle
	切换到JDK 11 sdk use java 11.0.0-open
	要设置默认值：
	
	默认为JDK 8 sdk default java 8.0.181-oracle
	默认为JDK 11 sdk default java 11.0.0-open

###  二、卸载
### 1. 卸载SDKMAN
打包备份要卸载的SDKMAN，防止后悔。删除SDKMAN安装路径。

	tar zcvf ~/sdkman-backup_$(date +%F-%kh%M).tar.gz -C ~/ .sdkman
	rm -rf ~/.sdkman

### 2. 还原.bash_profile
删除.bash_profile最后的

		THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
		[[ -s "/Users/你的用户名/.sdkman/bin/sdkman-init.sh" ]] && source "/
		Users/你的用户名/.sdkman/bin/sdkman-init.sh"



# JDK
### 1. 查看JDK版本
	/usr/libexec/java_home -V

### 2. 在Mac OS X下使用Homebrew安装jEnv：


	$ brew install jenv
	安装成功后需要进行一下简单的配置，让它可以起作用：
	//Bash
	$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
	$ echo 'eval "$(jenv init -)"' >> ~/.bash_profile
	
  	//Zsh
	$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
	$ echo 'eval "$(jenv init -)"' >> ~/.zshrc


### 3.好了，jEnv已经安装好了，让我们来看一下它找见哪个Java版本了：


	$ jenv versions
	* system (set by /Users/bxpeng/.jenv/version)
	它只找到了系统默认的Java，即使我已经下载了其他版本的Java。*表示当前选择的版本。
	
	和rbenv不同的是，jEnv不能自己安装任何版本的Java，所以需要我们手动安装好之后再用jEnv指向它们。
	
	安装Java 6，需要在Apple进行下载。它将安装到/System/Library/Java/JavaVirtualMachines/下； 安装Java 7，可以在Oracle进行下载.它将安装到/Library/Java/JavaVirtualMachines/下； 安装Java 8，可以在Oracle进行下载.它将安装到/Library/Java/JavaVirtualMachines/下。
	
	使用jenv add将Java 6加入jenv中：


	$ jenv add /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home/
	1.6 added
	1.6.0.65 added
	oracle64-1.6.0.65 added
	运行jenv versions时会显示：

	
	$ jenv versions
	* system (set by /Users/bxpeng/.jenv/version)
	  1.6
	  1.6.0.65
	  oracle64-1.6.0.65
	同样的，使用jenv add将Java 7加入jenv中：


	
	$ jenv add /Library/Java/JavaVirtualMachines/jdk1.7.0_71.jdk/Contents/Home/
	1.7 added
	1.7.0.71 added
	oracle64-1.7.0.71 added
	
	$ jenv add /Library/Java/JavaVirtualMachines/jdk1.8.0_25.jdk/Contents/Home/
	1.8 added
	1.8.0.25 added
	oracle64-1.8.0.25 added
	现在运行jenv versions会显示：


	$ jenv versions
	* system (set by /Users/bxpeng/.jenv/version)
	  1.6
	  1.6.0.65
	  oracle64-1.6.0.65
	  1.7
	  1.7.0.71
	  oracle64-1.7.0.71
	  1.8
	  1.8.0.25
	  oracle64-1.8.0.25
	对于博主这种不是处女座的人来说，也觉得需要对版本再管理一下，使用jenv remove可以从jEnv中去掉不需要的Java版本：

	
	$ jenv remove 1.6
	JDK 1.6 removed
	整理后，再运行jenv versions会显示：


	
	$ jenv versions
	* system (set by /Users/bxpeng/.jenv/version)
	  1.6.0.65
	  1.7.0.71
	  1.8.0.25
	选择一个Java版本，运行jenv local，例如：


	$ jenv local 1.8.0.25
	$ java -version
	java version "1.8.0_25"
	Java(TM) SE Runtime Environment (build 1.8.0_25-b17)
	Java HotSpot(TM) 64-Bit Server VM (build 25.25-b02, mixed mode)
	DangDangDangDang，我们已经成功地指定了某文件夹中local的Java版本。
	
	你可以运行jenv global设置一个默认的Java版本，运行jenv which java显示可执行的Java的完整路径。
	
	你也可以在特定的文件夹下使用.java-version文件来设定Java的版本。当我需要在Project中使用Java 6时，我仅仅需要把1.6.0.65作为内容保存在.java-version文件中，当我进入该文件夹时jEnv会自动地帮助我设定local的Java的版本。
	
	没错，我们现在有了Java的多个版本，并且可以在它们之间轻松切换。更多的使用方法可以在jEnv官网的官网查询到。


# 链接
[安装 Android Studio](https://developer.android.com/studio/install?hl=zh-cn)
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()
[]()