# Grpc Proto To Nuget Package 插件使用说明

> GrpcProtoToNugetPackage 是一个 VS 插件，目的是将基于 gRPC 的接口定义 .proto 文件一键转成 Nuget Package，然后发布到私有仓库上。 

1. 下载最新 [GrpcProtoToNugetPackageTemplate.zip](https://github.com/mingdaocom/GrpcProtoToNugetPackage/releases) ASP.NET 的项目模板，关于ASP.NET 的项目模板介绍可 [查看文章](http://beckjin.com/2019/08/04/aspnet-template/)  

1. 解压 GrpcProtoToNugetPackageTemplate.zip，进入目录执行 `dotnet new -i Grpc.Proto.To.Nuget.Package.1.0.0.nupkg` 进行模板安装 （以下为可选操作，但建议修改）
   
   > 对模板内的 `Content/.template.config/template.json`、`GrpcProtoToNugetPackage.csproj`、`Grpc.Proto.To.Nuget.Package.nuspec` 进行修改调整，如：`Authors`、`Company`、`RepositoryUrl` 参数的配置
   
   > 修改后需要通过 `nuget pack Grpc.Proto.To.Nuget.Package.nuspec`（将 nuget.exe 添加到环境变量） 重新生成 `Grpc.Proto.To.Nuget.Package.1.0.0.nupkg`
   
   > 然后重新安装项目模板


1. 安装成功后，可通过 `dotnew new -u` 进行查看模板，如下：`Grpc.Proto.To.Nuget.Package` 即刚刚安装的模板，如果要卸载，执行 `dotnew new -u Grpc.Proto.To.Nuget.Package`

   ![image](https://user-images.githubusercontent.com/7261408/62512104-34d4de80-b849-11e9-86c0-cbc6187d9599.png)

1. 下载最新版 [GrpcProtoToNugetPackage.vsix](https://github.com/mingdaocom/GrpcProtoToNugetPackage/releases)，在关闭所有 VS 窗口下，安装此插件（建议安装 VS2019）

1. 安装成功后，VS 打开一个含 `proto` 文件的项目（注意：`.proto` 文件必须放在 `protos` 文件夹下）

1. 在 `protos` 文件夹右键选择 `Grpc Proto To Nuget Package`

   ![image](https://user-images.githubusercontent.com/7261408/62517122-3dcdac00-b859-11e9-9119-95a8f2729898.png)

1. 弹出配置窗口，设置 Nuget Package 要推送到的 `源地址` 和 `APIKey`（首次需要设置，如：APIKey 可在 https://www.nuget.org/ 个人中心申请进行测试，实际私有的 Nuget Package 不应该推送到公共平台上）
   
   ![image](https://user-images.githubusercontent.com/7261408/62517465-06abca80-b85a-11e9-9596-eb86979599ad.png)
   
1. 输入包的版本号（目前需要手动输入）

   > 执行过程中使用的资源文件会暂存到 `C:\TempGrpcNuget` 目录下。首次会创建 `repository.json` 保存 Nuget 仓库的配置信息，接下来每次会根据包名创建一个临时项目用于生成对应 Nuget Package，如果有问题，一般是因不符合规范导致编译不通过，这时候可以将当前项目导入 VS 就行编译查看具体问题。

1. 执行，注意输出日志，确保推送到远端仓库 OK

   ![image](https://user-images.githubusercontent.com/7261408/62517775-ae28fd00-b85a-11e9-8ff8-2012e1a397f9.png)
