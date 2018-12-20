###安装
	xcode-select --install
	sudo gem install -n /usr/local/bin fastlane

### 蒲公英 fir




	fastlane add_plugin pgyer
	fastlane add_plugin versioning
	fastlane add_plugin firim
	
### gym和build_app都是build_ios_app的别名

	workspace : 使用cocoapods后的工程文件路径
	project : 项目文件路径
	scheme : 项目的白名单,在Manage schemes中将其设置为shared状态
	output_directory : 打包出来的ipa包存储的位置 .
	output_name : 打包出的ipa包名称
	configuration : 编译APP是的配置,默认是 release
	silent : 编译时隐藏不必要的信息,默认是false
	export_method : 打包的类型: app-store, ad-hoc, package, enterprise, development, developer-id
	export_options : 导出的选项设置,新Xcode允许导出时修改plist文件
	build_path : 打archive包的存储路径
	buildlog_path : 存储bulid的log
	sdk : 打包时使用的sdk
	
###	
	
	submission_information({
	  export_compliance_available_on_french_store: "false",
	  export_compliance_contains_proprietary_cryptography: "false",
	  export_compliance_contains_third_party_cryptography: "false",
	  export_compliance_is_exempt: "false",
	  export_compliance_uses_encryption: "false",
	  export_compliance_app_type: nil,
	  export_compliance_encryption_updated: "false",
	  export_compliance_compliance_required: "false",
	  export_compliance_platform: "ios",
	  content_rights_contains_third_party_content: "false",
	  content_rights_has_rights: "false",
	  add_id_info_limits_tracking: "true",
	  add_id_info_serves_ads: "false",
	  add_id_info_tracks_action: "true",
	  add_id_info_tracks_install: "true",
	  add_id_info_uses_idfa: "true"
	});

### 参考
[Fastlane自动打包工具build号自增处理配置方法,修改buildsettings里面的version配置，current project version 随便填一个。versionsystem 选择apple generic](https://www.jianshu.com/p/24da3f5bee3c)


[Fastlane自动打包上传iOS App](https://juejin.im/entry/59b796e9f265da06670c5a51)