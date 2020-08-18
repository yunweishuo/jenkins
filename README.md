# 基本说明

- 每个公司都有自己的运维规范及标准化，将根据实际公司标准化，定制jenkins安装包。
- 每个公司标准不一，仅供参考。

# 工具

- 使用TLS版本的jenkins war包
- 使用fpm工具进行安装包制作

# 目录规划

- WAR目录
    - /opt/websuite/jenkins
- 配置文件目录
    - /opt/config/jenkins
- PID文件目录
    - /opt/run/jenkins
- 日志文件目录
    - /opt/logs/jenkins
- 家目录
    - /opt/data/jenkins
- 启动脚本
    - /etc/init.d/jenkins
- 日志切割脚本
    - /etc/logrotate.d/jenkins

# 安装插件列表

- Localization: Chinese (Simplified) 
- Locale
```
以上两个插件用于配置中文插件
```

- Role-based Authorization Strategy
```
用于jenkins用户权限管理
```

- Credentials Binding插件
```
用于管理第三方账户信息，比如gitlab、ssh秘钥等
```

- Maven Integration
```
java项目，Maven插件
```

- Pipeline
```
使用流水线编写发布代码脚本
```


- Publish Over SSH
```
远程执行脚本插件
```

- SonarQube Scanner for Jenkins
```
代码质量检测插件
```

- Gitlab Hook
- Gitlab
```
以上两个插件可用于配置钩子，动态发布代码。
```

- Git
- Extended Choice Parameter
```
多个项目时，通过此插件勾选所需发布项目
```

- Email Extension Template
```
配置邮件通知插件
```

- MultiJob
```
可实现多任务编排
```


# 配置说明

## logrotate参数说明

>参考链接：https://blog.csdn.net/liuxiao723846/article/details/100120058

```
# cat /etc/logrotate.d/jenkins      
/opt/logs/jenkins/*.log { #切割目录下以log结尾的日志
    daily #日志轮询周期，每天
    compress #切割后压缩
    delaycompress #下次logratate进行分割操作时，再将本次分割的日志文件进行压缩
    dateext #日志文件切割时添加日期后缀
    missingok #如果日志文件不存在，也不报错
    rotate 30  #保存30天数据，超过的则删除
    ifempty #不论日志是否为空，都进行轮替
    create 644 #使用该权限创建日志文件
    copytruncate #将原始文件拷贝一份重命名，然后把原始文件清空
}
```

## jenkins用户权限管理
```
已将jenkins用户权限管理修改为Role-based Authorization Strategy
```
