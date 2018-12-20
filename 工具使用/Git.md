# git


1.常用指令

	1. git init 
	2. git add .
	3. git commit -m ''
	4. git commit -am ''

2.远程仓库

	1. git remote -v  # 查看所有远程仓库。--verbose 的简写，取首字母
	2. git remote add origin git://github.com/paulboone/ticgit.git
	3. git pull origin master
	4. git push origin master
	5. git remote show origin #查看某个远程仓库的详细信息，比如要看所克隆的 origin 仓库
	6. git remote rename pb paul # 远程仓库的删除和重命名
	7. git remote rm paulorigin
 	
 	
3.打标签

	1. git tag #列出现有标签
	2. git tag -a v1.4 -m 'my version 1.4' #含附注的标签
	3. git show v1.4.  # 查看相应标签的版本信息

4.分支
   
	1. git branch -a # 列出所有分支 本地和远程
	2. git push origin zhouzhi  # 推送本地分支zhouzhi
	3. git checkout --track origin/zhouzhi # 跟踪远程分支 即本地会有一个远程分支对应的本地分支
	4. git push origin [tagname] / git push origin --tags # 推送所有本地标签



# 绑定 项目（Lazy-Health-Client）

#### Git 全局设置
	git config --global user.name "周志"
	git config --global user.email "853489221@qq.com"

#### 创建新版本库
	git clone https://gitlab.lanrenyun.cn/Lazy-iOS/Lazy-Health-Client.git
	cd Lazy-Health-Client
	touch README.md
	git add README.md
	git commit -m "add README"
	git push -u origin master

#### 已存在的文件夹
	cd existing_folder
	git init
	git remote add origin https://gitlab.lanrenyun.cn/Lazy-iOS/Lazy-Health-Client.git
	git add .
	git commit -m "Initial commit"
	git push -u origin master
	git pull origin master --allow-unrelated-histories

#### 已存在的 Git 版本库

	cd existing_repo
	git remote add origin https://gitlab.lanrenyun.cn/Lazy-iOS/Lazy-Health-Client.git
	git push -u origin --all
	git push -u origin --tags

	



#常见问题
Commit的时候UserInterfaceState.xcuserstate这个文件几秒钟更新一次, 搅得人不得安宁, 用.gitignore无效. 于是, 在终端中输入:

git rm −−cache  diLedger.xcodeproj/project.xcworkspace/xcuserdata/Alex.xcuserdatad/UserInterfaceState.xcuserstate 

git commit -m "Removed the stupid strange file that shouldn't be tracked" 
$ git push




