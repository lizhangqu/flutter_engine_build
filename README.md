# flutter_engine_build

Flutter Engine 构建产物归档及构建辅助脚本，可用于持续集成环境，见 
 - [Flutter Engine 产物归档与符号表备份](https://fucknmb.com/2019/12/12/Flutter-Engine%E4%BA%A7%E7%89%A9%E5%BD%92%E6%A1%A3%E4%B8%8E%E7%AC%A6%E5%8F%B7%E8%A1%A8%E5%A4%87%E4%BB%BD/)

Usage:

```
./flutter_engine_build \
  --local-engine-src-path /path/to/engine/src \
  --no-ios \
  --no-android \
  --no-arm \
  --no-arm64 \
  --no-x86 \
  --no-x64 \ 
  --no-debug \
  --no-profile \
  --no-release \
  --gn \
  --clean \
  --build \
  --artifacts \
  --symbols
```


提示:
 - 如果你不需要执行iOS相关脚本，那么添加--no-ios参数，默认都会执行
 - 如果你不需要执行android相关脚本，那么添加--no-android参数，默认都会执行
 - 如果你不需要执行arm相关脚本，那么添加--no-arm参数，默认都会执行
 - 如果你不需要执行arm64相关脚本，那么添加--no-arm64参数，默认都会执行
 - 如果你不需要执行x86相关脚本，那么添加--no-x86参数，默认都会执行
 - 如果你不需要执行x64相关脚本，那么添加--no-x64参数，默认都会执行
 - 如果需要构建iOS模拟器产物，那么添加--x64参数，默认情况下就会执行，除非添加了--no-x64参数
 - 如果你不需要执行debug相关脚本，那么添加--no-debug参数，默认都会执行
 - 如果你不需要执行profile相关脚本，那么添加--no-profile参数，默认都会执行
 - 如果你不需要执行release相关脚本，那么添加--no-release参数，默认都会执行
 - 如果你需要调用gn生成Ninja配置文件，那么添加--gn参数，默认不会执行
 - 如果你需要调用Ninja执行clean，那么添加--clean参数，默认不会执行
 - 如果你需要调用Ninja执行build，那么添加--build参数，默认不会执行
 - **如果你需要按cache目录结构归档产物，那么添加--artifacts参数，默认不会执行**
 - **如果你需要归档符号表文件，那么添加--symbols参数，默认不会执行**
 - 以上参数为同时作用生效，即**与**的关系
 - 产物和符号表归档目录为/path/to/engine/src/out/engine/artifacts和/path/to/engine/src/out/engine/symbols下
 - iOS的产物归档需要同时构建完对应构建类型(debug，profile，release)下的arm，arm64，debug_sim产物，否则归档会失败
 
如果你需要构建iOS debug产物，并进行归档，同时备份符号表，则执行

```
./flutter_engine_build \
  --local-engine-src-path /path/to/engine/src \
  --no-android \
  --no-profile \
  --no-release \
  --gn \
  --clean \
  --build \
  --artifacts \
  --symbols
```

如果你需要构建Android profile arm64产物，并进行归档，同时备份符号表，则执行

```
./flutter_engine_build \
  --local-engine-src-path /path/to/engine/src \
  --no-ios \
  --no-debug \
  --no-release \
  --no-arm \
  --no-x86 \
  --no-x64 \
  --gn \
  --clean \
  --build \
  --artifacts \
  --symbols
```

如果你不需要执行Ninja构建，仅仅是归档iOS产物和符号表，则执行

```
./flutter_engine_build \
  --local-engine-src-path /path/to/engine/src \
  --no-android \
  --artifacts \
  --symbols
```

假如你执行如下命令

```
./flutter_engine_build \
  --local-engine-src-path /path/to/engine/src \
  --gn \
  --clean \
  --build \
  --artifacts \
  --symbols
```

那么android会执行的构建有：

debug-arm，debug-arm64，debug-x86，debug-x64，profile-arm，profile-arm64，release-arm，release-arm64

iOS会执行的构建有：

debug-arm，debug-arm64，debug-sim，profile-arm，profile-arm64，release-arm，release-arm64

并且会将产物和符号表进行归档
