# bugtagsAction
使用fastlane来做自动化，发现并不支持业务要求使用bugtags的action，添加了支持。

## 配置
```
下载bugtags.rb文件，导入到iOS工程目录下的fastlane/actions/目录的下
```

## 使用
```ruby
desc "打包并上传dsym文件到bugtags"
  lane :topgy do
    info_plist = ".../Info.plist"
    app_version = sh("/usr/libexec/PlistBuddy -c \"Print CFBundleShortVersionString\" \"#{info_plist}\"").chomp  
    app_build = sh("/usr/libexec/PlistBuddy -c \"Print CFBundleVersion\" \"#{info_plist}\"").chomp  

    gym(
      ...
    )
    
    bugtags(
      dsym: "your-dsym-path/xxx.app.dSYM.zip",
      app_key: "your-app-key",
      secret_key: "your-secret-key",
      app_version: "#{app_version}",
      app_build: "#{app_build}", 
    )
end
```

