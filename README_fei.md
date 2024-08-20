1、服务端：

项目数据库文件 storage/data/hotgo.sql 创建数据库并导入
将配置文件 manifest/config/config.yaml.bak 复制后改为manifest/config/config.yaml
将manifest/config/config.yaml中的database.default.link数据库配置改为你自己的：
# Database. 配置参考：https://goframe.org/pages/viewpage.action?pageId=1114245
database:
  logger:
    path: "logs/database"                       # 日志文件路径。默认为空，表示关闭，仅输出到终端
    <<: *defaultLogger
    stdout: true
  default:
    link: "mysql:hotgo:hg123456.@tcp(127.0.0.1:3306)/hotgo?loc=Local&parseTime=true&charset=utf8mb4"
    debug: true
    Prefix: "hg_"
将hack/config.yaml中的gfcli.gen.dao[0].link数据库配置改为你自己的：
gfcli:
  gen:
    dao:
      - link: "mysql:hotgo:hg123456.@tcp(127.0.0.1:3306)/hotgo?loc=Local&parseTime=true&charset=utf8mb4"
        group: "default"                                                # 分组 使用hotgo代码生成功能时必须填
        #        tables:          ""                                    # 指定当前数据库中需要执行代码生成的数据表。如果为空，表示数据库的所有表都会生成。
        tablesEx:        "hg_sys_addons_install"                        # 指定当前数据库中需要排除代码生成的数据表。
        removePrefix: "hg_"
        descriptionTag: true
        noModelComment: true
        jsonCase: "CamelLower"
        gJsonSupport: true
        clear: false

1、服务端：

      cd server
      
      # 设置国内代理，如果已经设置好了代理可以跳过
      go env -w GOPROXY=https://goproxy.io,direct
      
      # 更新包
      go mod tidy  
      
      # 查看命令行方法
      go run main.go help
      
      # 启动所有服务
      go run main.go  # 热编译启动： gf run main.go
2、web前端：

    cd web
    # 首先确定你以安装node16.0以上版本并安装了包[npm、yarn]，否则可能会出现一些未知报错
    
    # 安装依赖
    yarn install 
    
    # 启动web项目
    yarn dev 
    
    # 如果顺利，至此到浏览器打开：http://你的IP:8001/admin
    # 登录账号：admin, 密码：123456


    前端安装会有的问题

这个错误是由于 PowerShell 的执行策略设置阻止了脚本运行。默认情况下，Windows 可能会限制脚本的执行，以防止不安全的脚本运行。

解决方法：
1. 临时允许脚本执行
你可以通过以下步骤临时允许脚本执行，然后再恢复默认设置：

以管理员身份运行 PowerShell：

右键点击开始菜单，选择“Windows PowerShell (管理员)”或“Windows PowerShell Admin”。
修改执行策略：

在 PowerShell 中输入以下命令，允许当前会话运行脚本：
powershell
复制代码
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
然后再运行 yarn install。
恢复默认执行策略：

安装完成后，关闭 PowerShell，或者在当前会话中输入以下命令以恢复默认执行策略：
powershell
复制代码
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Default
2. 永久修改执行策略（不推荐）
如果你希望永久性地允许脚本执行，可以设置系统级别的执行策略：

以管理员身份运行 PowerShell。

设置执行策略：

powershell
复制代码
Set-ExecutionPolicy RemoteSigned
这会允许运行本地脚本和由受信任发布者签名的远程脚本。

确认设置：

PowerShell 可能会提示你确认更改，输入 Y 并按回车键。