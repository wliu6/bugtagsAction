# bugtagsAction

## 配置
```
下载bugtags.rb文件，导入到iOS工程目录下的fastlane/actions/目录的下
```

## 使用
```ruby
desc "打包到蒲公英"
  lane :topgy do
    info_plist = "/Users/wangduorui/kszc_work/kszc_wsp/KaiShiBa_iOS/kaistart/kaistart/Info.plist"
    app_version = sh("/usr/libexec/PlistBuddy -c \"Print CFBundleShortVersionString\" \"#{info_plist}\"").chomp  
    app_build = sh("/usr/libexec/PlistBuddy -c \"Print CFBundleVersion\" \"#{info_plist}\"").chomp  

    gym(
      clean:true,
      silent: true,
      export_method:"development",
      scheme: "kaiStart-Adhoc",
      configuration: "Adhoc",
      archive_path:"./app",
      output_directory:"./app",
      output_name:"kaiStart-Adhoc",
    )
    
    pgyer(
      api_key: "6444c88bb134932a1942a14cab78836d", 
      user_key: "486fa87c6852d447985b5beefc8f2143",
      update_description: "update by fastlane"
    )

    bugtags(
      dsym: "/Users/wangduorui/kszc_work/kszc_wsp/KaiShiBa_iOS/kaistart/app/kaiStart-Adhoc.app.dSYM.zip",
      app_key: "2e9ca24801df12be6a1b312261156058",
      secret_key: "f60747a14b55992c99d41e864894661f",
      app_version: "#{app_version}",
      app_build: "#{app_build}", 
    )
end
```

