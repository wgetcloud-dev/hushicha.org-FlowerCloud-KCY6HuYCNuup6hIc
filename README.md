
目录* [1\. 概论](https://github.com)
* [2\. 详论](https://github.com)
	+ [2\.1 创建工程](https://github.com)
	+ [2\.2 加载工程](https://github.com)
	+ [2\.3 配置文件](https://github.com):[飞数机场](https://ze16.com)
	+ [2\.4 工程配置](https://github.com)
	+ [2\.5 调试执行](https://github.com)
* [3\. 项目案例](https://github.com)
* [4\. 总结](https://github.com)

# 1\. 概论


在之前的系列博文中，我们学习了如何构建第三方的依赖库，也学习了如何去组建自己的CMake项目，尤其是学习了CMake的核心配置文件CMakeLists.txt如何编写。长期以来，CMakeLists.txt这个文件都是C/C\+\+项目额外编写的，然后使用CMake指令或者GUI工具配置成Windows下的MSVC工程，或者Linux下的Makefile文件。这样做虽然对比之前需要不同的平台下要使用不同的工程有了长足的进步，但是还可以再进一步，那就是直接在IDE中使用CMake工程进行开发，这样无疑对C/C\+\+程序开发的效率有质的提升。


从Visual Studio 2017开始，Microsoft Visual Studio（简称VS）就开始支持CMake工程的导入。所谓CMake工程，指的就是不再需要建立传统的MSVC项目，例如.sln或者.vcxproj工程文件，而是直接使用CMakeLists.txt作为工程配置文件来进行加载，进行进行构建和开发的工作。不仅是VS，目前其他IDE比如Visual Studio Code、Qt Creator、IntelliJ IDEA、 CLion都能直接支持CMake工程的导入。但是，作为初学者，笔者还是建议从Microsoft Visual Studio入手进行CMake项目的开发，毕竟号称宇宙第一的IDE不是白叫的。以笔者的观点来看，Microsoft Visual Studio的确实有点重，编辑器也不是最美观的，UI操作也不一定是最人性化的，但是其提供的调试功能却是最优秀且不可或缺的，尤其适合商业中的生产力环境。这里笔者就以Visual Studio 2019 为例，详细讲解一下如何进行CMake项目的开发，以提升我们的C/C\+\+程序开发效率。


# 2\. 详论


## 2\.1 创建工程


启动Visual Studio 2019，弹出的启动页面，如下图1所示：


![图1：Visual Studio 2019启动页面](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212337927-913098526.png)


点击右下方“创建新项目”按钮，进入“创建新项目”页面，如下图2所示：


![图2：创建新项目页面](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212413150-1446278782.png)


选择“CMake项目”的模板，如果没有看到可以搜索一下模板。点击“下一步”按钮，进入“配置新项目”页面，如下图3所示：


![图3：配置新项目页面](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212440853-594707286.png)


在“配置新项目”页面填入项目名称和位置，点击“创建”按钮，就进入了Visual Studio 2019的主要工作页面，如下图4所示：


![图4：主要工作页面](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212500550-793723088.png)


## 2\.2 加载工程


关闭Visual Studio 2019，模拟一下直接加载现有CMake工程的情况。再次启动Visual Studio 2019，一般在图1所示的启动页面中可以看到上次加载过的历史记录，点击就可以再次进行加载了。但是如何没有历史记录，就点击“继续但无需代码”按钮，直接进入主页面。在菜单栏中依次选择文件\-\>打开\-\>CMake按钮，如下图5所示：


![图5：加载CMake工程入口](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212523173-1160392006.png)


此时会弹出“打开CMake项目”对话框，选中项目中的CMakeList.txt文件，CMake项目就是通过这个核心配置文件来打开的，如下图6所示：


![图6：选择CMakeList.txt文件](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212542554-1825135939.png)


记住一定要通过这种方式打开CMakeList.txt文件才会打开CMake项目，如果直接将CMakeList.txt文件拖入到Visual Studio 2019主页面中只会文本形式显示CMakeList.txt。


## 2\.3 配置文件


接下来再正式进行开发之前，我们需要先搞定一个配置文件CMakePresets.json。CMakeList.txt具有非常多的配置项，或者需要传入的外部参数，需要使用一个配置文件来进行管理。不过麻烦就麻烦在这里，CMakePresets.json是CMake 3\.20引入的，是个相对较新的功能，Visual Studio 2019并没有一开始就对接这个配置文件，而是使用自己设计的CMakeSettings.json文件作为CMake构建项目的配置。目前，这两种配置文件Visual Studio 2019都支持，但是更推荐使用CMakePresets.json，因为更加标准化，符合CMake的规范，可以被多种IDE和构建工具识别和支持。


具体来说，如果程序主页面，尤其是主页面的工具栏与下图7有所不同：


![图7：CMake项目的工具栏](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212558711-2042141219.png)


那么可以在菜单栏依次选择工具\-\>选项\-\>CMake\-\>常规，勾选“首次使用CMake预设值进行配置、构建和测试”的单选框，如下图8所示：


![图8：设置CMake预设配置](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212615016-1226187240.png)


点击工具栏的配置下拉菜单，选择“管理配置”按钮，如下图9所示：


![图9：管理配置](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212631317-1538910750.png)


此时Visual Studio 2019就会自动创建CMakeSettings.json配置文件，如下图10所示：


![图10：CMakeSettings.json配置文件](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212646756-2043746491.png)


从这个文件可以看到默认的windows\-default配置其实是Debug模式，我们可以将其增加一个RelWithDebInfo模式，也就是Release带调试信息模式，CMakePresets.json具体的内容为：



```
{
  "version": 2,
  "configurePresets": [
    {
      "name": "linux-default",
      "displayName": "Linux Debug",
      "description": "面向适用于 Linux 的 Windows 子系统(WSL)或远程 Linux 系统。",
      "generator": "Ninja",
      "binaryDir": "${sourceDir}/out/build/${presetName}",
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "Debug",
        "CMAKE_INSTALL_PREFIX": "${sourceDir}/out/install/${presetName}"
      },
      "vendor": {
        "microsoft.com/VisualStudioSettings/CMake/1.0": { "hostOS": [ "Linux" ] },
        "microsoft.com/VisualStudioRemoteSettings/CMake/1.0": { "sourceDir": "$env{HOME}/.vs/$ms{projectDirName}" }
      }
    },
    {
      "name": "windows-default",
      "displayName": "Windows x64 Debug",
      "description": "面向具有 Visual Studio 开发环境的 Windows。",
      "generator": "Ninja",
      "binaryDir": "${sourceDir}/out/build/${presetName}",
      "architecture": {
        "value": "x64",
        "strategy": "external"
      },
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "Debug",
        "CMAKE_INSTALL_PREFIX": "${sourceDir}/out/install/${presetName}"
      },
      "vendor": { "microsoft.com/VisualStudioSettings/CMake/1.0": { "hostOS": [ "Windows" ] } }
    },
    {
      "name": "RelWithDebInfo",
      "displayName": "Windows x64 RelWithDebInfo Shared Library",
      "description": "面向具有 Visual Studio 开发环境的 Windows。",
      "generator": "Ninja",
      "binaryDir": "${sourceDir}/out/build/${presetName}",
      "architecture": {
        "value": "x64",
        "strategy": "external"
      },
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "RelWithDebInfo",
        "CMAKE_INSTALL_PREFIX": "${sourceDir}/out/install/${presetName}"
      },
      "vendor": { "microsoft.com/VisualStudioSettings/CMake/1.0": { "hostOS": [ "Windows" ] } }
    }
  ]
}

```

添加这段配置并Ctrl\+S保存之后，工具栏的配置下拉菜单就会多了RelWithDebInfo这个选项，将其选中，如下图11所示：


![图11：选中配置](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212703652-225768669.png)


注意，有的时候因为两种配置方式的冲突问题，会导致一些异常现象，比如工具栏的配置菜单不太一样。如果遇到这种情况可以推出Visual Studio 2019，清理工程的中间生成文件，再重新加载工程试试。


## 2\.4 工程配置


再接下来的步骤不要急着去编写源代码文件，要先完成CMakeLists.txt的编写。新建工程的CMakeLists.txt会有一段默认的内容，如下所示：



```
# CMakeList.txt: ZipTest 的 CMake 项目，在此处包括源代码并定义
# 项目特定的逻辑。
#
cmake_minimum_required (VERSION 3.8)

project ("ZipTest")

# 将源代码添加到此项目的可执行文件。
add_executable (ZipTest "ZipTest.cpp" "ZipTest.h")

# TODO: 如有需要，请添加测试并安装目标。

```

如果我们学习过上一篇博文的话就会理解这段配置代码文件，推荐读者复习一下。这里要说的关键是，在修改CMakeLists.txt文件之后，需要Ctrl\+S保存一下，Visual Studio 2019就会自动进行工程配置，可以在输出窗口看到一些输出信息：



```
1> 已为配置“RelWithDebInfo”启动 CMake 生成。
1> 环境设置:
1>     CommandPromptType=Native
1>     DevEnvDir=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\
1>     ExtensionSdkDir=C:\Program Files (x86)\Microsoft SDKs\Windows Kits\10\ExtensionSDKs
1>     Framework40Version=v4.0
1>     FrameworkDir=C:\windows\Microsoft.NET\Framework64\
1>     FrameworkDIR64=C:\windows\Microsoft.NET\Framework64
1>     FrameworkVersion=v4.0.30319
1>     FrameworkVersion64=v4.0.30319
1>     HTMLHelpDir=C:\Program Files (x86)\HTML Help Workshop
1>     IFCPATH=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\ifc\x64
1>     IGCCSVC_DB=AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAggkwNDDGDkq0HFOUjEsXQAQAAAACAAAAAAAQZgAAAAEAACAAAADxjk35GiqLjZDHeYjx5dq8wxmbU7aEbBW9J68TO/bzIwAAAAAOgAAAAAIAACAAAADdM3gyHGrxXOwEEyHmxfe9ocZnP6CM0OTQGZYVZKgQWmAAAAC8xGVDuFoU062/gozauvaMPUmsT8FAuEXoLnI9lTwHVT6XWpjF7lVBoYB+vxo1dgIUAtW0nl1wZSUg9KRxmYpIicPPLm7B+twKXEdbaDMIu55E10uazKjjvoHY/4KYu+tAAAAAoK95FWIYAE3f+YLjfb3S77+ZMJXFw69cRlxyTYekzkyfOFdUcCY94ahV+XHEgao2y8e/zT+q2zHU0SqXho0LDQ==
1>     INCLUDE=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\ATLMFC\include;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\include;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.8\include\um;C:\Program Files (x86)\Windows Kits\10\include\10.0.22000.0\ucrt;C:\Program Files (x86)\Windows Kits\10\include\10.0.22000.0\shared;C:\Program Files (x86)\Windows Kits\10\include\10.0.22000.0\um;C:\Program Files (x86)\Windows Kits\10\include\10.0.22000.0\winrt;C:\Program Files (x86)\Windows Kits\10\include\10.0.22000.0\cppwinrt
1>     LIB=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\ATLMFC\lib\x64;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\lib\x64;C:\Program Files (x86)\Windows Kits\NETFXSDK\4.8\lib\um\x64;C:\Program Files (x86)\Windows Kits\10\lib\10.0.22000.0\ucrt\x64;C:\Program Files (x86)\Windows Kits\10\lib\10.0.22000.0\um\x64
1>     LIBPATH=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\ATLMFC\lib\x64;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\lib\x64;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\lib\x86\store\references;C:\Program Files (x86)\Windows Kits\10\UnionMetadata\10.0.22000.0;C:\Program Files (x86)\Windows Kits\10\References\10.0.22000.0;C:\windows\Microsoft.NET\Framework64\v4.0.30319
1>     NETFXSDKDir=C:\Program Files (x86)\Windows Kits\NETFXSDK\4.8\
1>     Path=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\\Extensions\Microsoft\IntelliCode\CLI;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\bin\HostX64\x64;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\VC\VCPackages;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\TestWindow;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\TeamFoundation\Team Explorer;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\MSBuild\Current\bin\Roslyn;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Team Tools\Performance Tools\x64;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Team Tools\Performance Tools;C:\Program Files (x86)\Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools\vs2019\\x64;C:\Program Files (x86)\Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools\vs2019\;C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools\x64\;C:\Program Files (x86)\HTML Help Workshop;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\Tools\devinit;C:\Program Files (x86)\Windows Kits\10\bin\10.0.22000.0\x64;C:\Program Files (x86)\Windows Kits\10\bin\x64;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\\MSBuild\Current\Bin;C:\windows\Microsoft.NET\Framework64\v4.0.30319;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\Tools\;C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\windows\system32;C:\windows;C:\windows\System32\Wbem;C:\windows\System32\WindowsPowerShell\v1.0\;C:\windows\System32\OpenSSH\;C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common;C:\Program Files\NVIDIA Corporation\NVIDIA NvDLISR;C:\Users\Administrator\AppData\Local\Microsoft\WindowsApps;C:\Program Files\HP\OMEN-Broadcast\Common;C:\Program Files\CMake\bin;C:\Program Files\Microsoft SQL Server\130\Tools\Binn\;C:\Program Files\TortoiseGit\bin;C:\Work\3rdparty\bin;C:\SoftWare\Qt\Qt5.12.5\5.12.5\msvc2017_64\bin;C:\File\MyGitHub\GISBasic\3rdParty\bin;C:\Program Files\dotnet\;C:\Work\eGova3rdParty\protobuf\bin;C:\Program Files\Java\jdk1.8.0_271\bin;C:\Program Files\KTX-Software\bin;C:\SoftWare\sonar-scanner-msbuild;C:\Program Files\Cppcheck;C:\SoftWare\sonar-scanner-msbuild\sonar-scanner-4.7.0.2747\bin;C:\SoftWare\apache-ant-1.10.8\bin;C:\Program Files (x86)\pcsuite\;C:\SoftWare\apache-maven-3.6.2\bin;C:\Program Files\7-Zip;C:\Program Files\Git\cmd;C:\SoftWare\nvm;C:\Program Files\nodejs;C:\SoftWare\Python\Python311\Scripts\;C:\SoftWare\Python\Python311\;C:\Users\Charlee\AppData\Local\Microsoft\WindowsApps;C:\Program Files\Microsoft VS Code\bin;C:\Users\Charlee\AppData\Local\GitHubDesktop\bin;C:\Users\Charlee\AppData\Roaming\npm;C:\SoftWare\nvm;C:\Program Files\nodejs;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\CMake\Ninja;C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\VC\Linux\bin\ConnectionManagerExe
1>     PROMPT=$P$G
1>     UCRTVersion=10.0.22000.0
1>     UniversalCRTSdkDir=C:\Program Files (x86)\Windows Kits\10\
1>     VCIDEInstallDir=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\VC\
1>     VCINSTALLDIR=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\
1>     VCToolsInstallDir=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Tools\MSVC\14.29.30133\
1>     VCToolsRedistDir=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\VC\Redist\MSVC\14.29.30133\
1>     VCToolsVersion=14.29.30133
1>     VS160COMNTOOLS=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\Tools\
1>     VSCMD_ARG_app_plat=Desktop
1>     VSCMD_ARG_HOST_ARCH=x64
1>     VSCMD_ARG_no_logo=1
1>     VSCMD_ARG_TGT_ARCH=x64
1>     VSCMD_DEBUG=5 
1>     VSCMD_VER=16.11.29
1>     VSINSTALLDIR=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\
1>     WindowsLibPath=C:\Program Files (x86)\Windows Kits\10\UnionMetadata\10.0.22000.0;C:\Program Files (x86)\Windows Kits\10\References\10.0.22000.0
1>     WindowsSdkBinPath=C:\Program Files (x86)\Windows Kits\10\bin\
1>     WindowsSdkDir=C:\Program Files (x86)\Windows Kits\10\
1>     WindowsSDKLibVersion=10.0.22000.0\
1>     WindowsSdkVerBinPath=C:\Program Files (x86)\Windows Kits\10\bin\10.0.22000.0\
1>     WindowsSDKVersion=10.0.22000.0\
1>     WindowsSDK_ExecutablePath_x64=C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools\x64\
1>     WindowsSDK_ExecutablePath_x86=C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools\
1>     __devinit_path=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\Tools\devinit\devinit.exe
1>     __DOTNET_ADD_64BIT=1
1>     __DOTNET_PREFERRED_BITNESS=64
1>     __VSCMD_PREINIT_PATH=C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\windows\system32;C:\windows;C:\windows\System32\Wbem;C:\windows\System32\WindowsPowerShell\v1.0\;C:\windows\System32\OpenSSH\;C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common;C:\Program Files\NVIDIA Corporation\NVIDIA NvDLISR;C:\Users\Administrator\AppData\Local\Microsoft\WindowsApps;C:\Program Files\HP\OMEN-Broadcast\Common;C:\Program Files\CMake\bin;C:\Program Files\Microsoft SQL Server\130\Tools\Binn\;C:\Program Files\TortoiseGit\bin;C:\Work\3rdparty\bin;C:\SoftWare\Qt\Qt5.12.5\5.12.5\msvc2017_64\bin;C:\File\MyGitHub\GISBasic\3rdParty\bin;C:\Program Files\dotnet\;C:\Work\eGova3rdParty\protobuf\bin;C:\Program Files\Java\jdk1.8.0_271\bin;C:\Program Files\KTX-Software\bin;C:\SoftWare\sonar-scanner-msbuild;C:\Program Files\Cppcheck;C:\SoftWare\sonar-scanner-msbuild\sonar-scanner-4.7.0.2747\bin;C:\SoftWare\apache-ant-1.10.8\bin;C:\Program Files (x86)\pcsuite\;C:\SoftWare\apache-maven-3.6.2\bin;C:\Program Files\7-Zip;C:\Program Files\Git\cmd;C:\SoftWare\nvm;C:\Program Files\nodejs;C:\SoftWare\Python\Python311\Scripts\;C:\SoftWare\Python\Python311\;C:\Users\Charlee\AppData\Local\Microsoft\WindowsApps;C:\Program Files\Microsoft VS Code\bin;C:\Users\Charlee\AppData\Local\GitHubDesktop\bin;C:\Users\Charlee\AppData\Roaming\npm;C:\SoftWare\nvm;C:\Program Files\nodejs
1>     __VSCMD_script_err_count=0
1>     HOMEPATH=\Users\Charlee
1>     DriverData=C:\Windows\System32\Drivers\DriverData
1>     COMPUTERNAME=LAPTOP-K38HMG48
1>     CommonProgramFiles(x86)=C:\Program Files (x86)\Common Files
1>     POSTGIS_GDAL_ENABLED_DRIVERS=ENABLE_ALL
1>     ProgramW6432=C:\Program Files
1>     OneDrive=C:\Users\Charlee\OneDrive
1>     __PSLockDownPolicy=0
1>     RegionCode=APJ
1>     DEVECOSTUDIO_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\devecostudio.vmoptions
1>     VisualStudioEdition=Microsoft Visual Studio Enterprise 2019
1>     WEBIDE_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\webide.vmoptions
1>     ServiceHubLogSessionKey=3AFDCD75
1>     PROCESSOR_REVISION=b701
1>     PROCESSOR_IDENTIFIER=Intel64 Family 6 Model 183 Stepping 1, GenuineIntel
1>     PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
1>     PkgDefApplicationConfigFile=C:\Users\Charlee\AppData\Local\Microsoft\VisualStudio\16.0_36d14652\devenv.exe.config
1>     JETBRAINS_CLIENT_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\jetbrains_client.vmoptions
1>     PROJ_LIB=C:\Program Files\PostgreSQL\16\share\contrib\postgis-3.4\proj
1>     CURL_CA_BUNDLE=C:\Program Files\PostgreSQL\16\ssl\certs\ca-bundle.crt
1>     TMP=C:\Users\Charlee\AppData\Local\Temp
1>     DATAGRIP_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\datagrip.vmoptions
1>     TEMP=C:\Users\Charlee\AppData\Local\Temp
1>     LOCALAPPDATA=C:\Users\Charlee\AppData\Local
1>     PUBLIC=C:\Users\Public
1>     eGova3rdParty=C:\Work\3rdparty
1>     GDAL_DATA=C:\Program Files\PostgreSQL\16\gdal-data
1>     PSModulePath=C:\Program Files\WindowsPowerShell\Modules;C:\windows\system32\WindowsPowerShell\v1.0\Modules
1>     ProgramData=C:\ProgramData
1>     JAVA_HOME=C:\Program Files\Java\jdk1.8.0_271
1>     USERDOMAIN=LAPTOP-K38HMG48
1>     platformcode=M7
1>     PROCESSOR_LEVEL=6
1>     NUMBER_OF_PROCESSORS=32
1>     PHPSTORM_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\phpstorm.vmoptions
1>     STUDIO_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\studio.vmoptions
1>     VSAPPIDDIR=C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\
1>     ProgramFiles(x86)=C:\Program Files (x86)
1>     FPS_BROWSER_USER_PROFILE_STRING=Default
1>     CommonProgramFiles=C:\Program Files (x86)\Common Files
1>     VS140COMNTOOLS=C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools\
1>     USERDOMAIN_ROAMINGPROFILE=LAPTOP-K38HMG48
1>     VisualStudioDir=C:\Users\Charlee\Documents\Visual Studio 2019
1>     IGCCSVC_DB=AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAggkwNDDGDkq0HFOUjEsXQAQAAAACAAAAAAAQZgAAAAEAACAAAADxjk35GiqLjZDHeYjx5dq8wxmbU7aEbBW9J68TO/bzIwAAAAAOgAAAAAIAACAAAADdM3gyHGrxXOwEEyHmxfe9ocZnP6CM0OTQGZYVZKgQWmAAAAC8xGVDuFoU062/gozauvaMPUmsT8FAuEXoLnI9lTwHVT6XWpjF7lVBoYB+vxo1dgIUAtW0nl1wZSUg9KRxmYpIicPPLm7B+twKXEdbaDMIu55E10uazKjjvoHY/4KYu+tAAAAAoK95FWIYAE3f+YLjfb3S77+ZMJXFw69cRlxyTYekzkyfOFdUcCY94ahV+XHEgao2y8e/zT+q2zHU0SqXho0LDQ==
1>     GISBasic=C:\File\MyGitHub\GISBasic\3rdParty
1>     VSLS_SESSION_KEEPALIVE_INTERVAL=0
1>     MAVEN_HOME=C:\SoftWare\apache-maven-3.6.2
1>     ProgramFiles=C:\Program Files (x86)
1>     RUBYMINE_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\rubymine.vmoptions
1>     APPCODE_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\appcode.vmoptions
1>     FPS_BROWSER_APP_PROFILE_STRING=Internet Explorer
1>     VSSKUEDITION=Enterprise
1>     OnlineServices=Online Services
1>     ThreadedWaitDialogDpiContext=-4
1>     IDEA_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\idea.vmoptions
1>     WEBSTORM_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\webstorm.vmoptions
1>     GOLAND_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\goland.vmoptions
1>     NVM_SYMLINK=C:\Program Files\nodejs
1>     NVM_HOME=C:\SoftWare\nvm
1>     SESSIONNAME=Console
1>     VisualStudioVersion=16.0
1>     SystemRoot=C:\windows
1>     CommonProgramW6432=C:\Program Files\Common Files
1>     ZES_ENABLE_SYSMAN=1
1>     LOGONSERVER=\\LAPTOP-K38HMG48
1>     VSAPPIDNAME=devenv.exe
1>     USERPROFILE=C:\Users\Charlee
1>     MSBuildLoadMicrosoftTargetsReadOnly=true
1>     QtMsBuild=C:\Users\Charlee\AppData\Local\QtMsBuild
1>     POSTGIS_ENABLE_OUTDB_RASTERS=1
1>     VSLANG=2052
1>     RIDER_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\rider.vmoptions
1>     APPDATA=C:\Users\Charlee\AppData\Roaming
1>     HOMEDRIVE=C:
1>     DATASPELL_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\dataspell.vmoptions
1>     GATEWAY_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\gateway.vmoptions
1>     CLION_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\clion.vmoptions
1>     JETBRAINSCLIENT_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\jetbrainsclient.vmoptions
1>     USERNAME=Charlee
1>     PROCESSOR_ARCHITEW6432=AMD64
1>     EFC_20336=1
1>     PROCESSOR_ARCHITECTURE=x86
1>     OS=Windows_NT
1>     ComSpec=C:\windows\system32\cmd.exe
1>     PYCHARM_VM_OPTIONS=C:\SoftWare\ideaI-windows\2023\vmoptions\pycharm.vmoptions
1>     SystemDrive=C:
1>     windir=C:\windows
1>     ALLUSERSPROFILE=C:\ProgramData
1> 命令行: "C:\windows\system32\cmd.exe" /c "%SYSTEMROOT%\System32\chcp.com 65001 >NUL && "C:\PROGRAM FILES (X86)\MICROSOFT VISUAL STUDIO\2019\ENTERPRISE\COMMON7\IDE\COMMONEXTENSIONS\MICROSOFT\CMAKE\CMake\bin\cmake.exe"  -G "Ninja"  -DCMAKE_BUILD_TYPE:STRING="RelWithDebInfo" -DCMAKE_INSTALL_PREFIX:STRING="C:/Work/ZipTest/out/install/RelWithDebInfo"  -DCMAKE_MAKE_PROGRAM="C:\PROGRAM FILES (X86)\MICROSOFT VISUAL STUDIO\2019\ENTERPRISE\COMMON7\IDE\COMMONEXTENSIONS\MICROSOFT\CMAKE\Ninja\ninja.exe" "C:\Work\ZipTest" 2>&1"
1> 工作目录: C:/Work/ZipTest/out/build/RelWithDebInfo
1> [CMake] -- Configuring done
1> [CMake] -- Generating done
1> [CMake] -- Build files have been written to: C:/Work/ZipTest/out/build/RelWithDebInfo
1> 已提取 CMake 变量。
1> 已提取源文件和标头。
1> 已提取代码模型。
1> 已提取工具链配置。
1> 已提取包含路径。
1> CMake 生成完毕。

```

这个配置工程的步骤一定不能少，且要保证看到“CMake生成完毕”的提示。如果生成中断的话，可以在输出日志中看到出错的地方并进行修改。本质上来说，CMakeLists.txt只是个文本文件而已，要通过这一步将构建的环境准备好，生成一些缓存文件和中间文件，从而便于构建工具链识别进行下一步作业。


## 2\.5 调试执行


在保证CMake配置工程完毕之后，就可以进行调试运行了。这一步的功能就无缝对接MSVC项目了，例如编辑代码，F7生成，F5调试，Ctrl\+F5执行，F9断点，F10逐过程调试以及F11逐语句调试。不过有一点要注意，就是要选择启动项，不然可能无法运行项目。具体可以在工具栏的选择启动项下拉菜单中，如下图12所示：


![图12：选择启动项](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212728047-1671430742.png)


我们当然要选中ZipTest.exe这个目标，不过一定要注意，只有当CMake生成完毕以后才会出现这个选项。如果没有这个选项，那就说明之前的CMake生成没有成功。


另外一个很实用的功能是，在CMake生成成功以后，可以切换到CMake目标项目。具体通过“解决资源管理器视图”的工具栏上的“在解决方案和可用视图之间切换”按钮进入，如下图13所示：


![图13：切换视图](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212742954-1013344595.png)


这个视图看起来有点像MSVC工程了，比文件夹视图简洁介多了。更重要的是由这个视图的右键菜单功能更实用一点，比如“设为启动项”按钮也可以实现上面的选择启动项功能。另外还有“添加”功能，与MSVC项目的“添加”功能类似，可以新建源代码文件加入到CMake工程中。不过这个功能是通过修改CMakeList.txt文件来实现的，读者可以自己试用一下。


![图14：CMake目标视图](https://img2024.cnblogs.com/blog/1000410/202409/1000410-20240914212758504-738518311.png)


其实笔者感觉这个CMake目标视图是想像MSVC工程一样，集成更多的常用GUI操作的功能，使得开发编程的效率更高。不过目前这些还只是半成品，比如这个“添加”功能是可以实现源代码文件的添加了，但是对应修改CMakeList.txt的内容不一定是我们想要的，关于这一点读者可以试用一段时间之后再领会。目前很多常用的IDE功能还是需要我们自己编辑CMakeList.txt文件来实现，尽管如此，已经可以帮助我们提升很大一部分开发效率了。


# 3\. 项目案例


默认的Hello CMake案例还是太简单了，我们还是将上一篇的调用libzip压缩文件和文件夹的案例用上。项目目录如下：



```
ZipTest
│   main.cpp
│   CMakeLists.txt    
|   CMakePresets.json

```

main.cpp的内容如下：



```
#include 

#include 
#include 
#include 

using namespace std;

void CompressFile2Zip(std::filesystem::path unZipFilePath,
                      const char* relativeName, zip_t* zipArchive) {
  std::ifstream file(unZipFilePath, std::ios::binary);
  file.seekg(0, std::ios::end);
  size_t bufferSize = file.tellg();
  char* bufferData = (char*)malloc(bufferSize);

  file.seekg(0, std::ios::beg);
  file.read(bufferData, bufferSize);

  //第四个参数如果非0，会自动托管申请的资源，直到zip_close之前自动销毁。
  zip_source_t* source =
      zip_source_buffer(zipArchive, bufferData, bufferSize, 1);

  if (source) {
    if (zip_file_add(zipArchive, relativeName, source, ZIP_FL_OVERWRITE) < 0) {
      std::cerr << "Failed to add file " << unZipFilePath
                << " to zip: " << zip_strerror(zipArchive) << std::endl;
      zip_source_free(source);
    }
  } else {
    std::cerr << "Failed to create zip source for " << unZipFilePath << ": "
              << zip_strerror(zipArchive) << std::endl;
  }
}

void CompressFile(std::filesystem::path unZipFilePath,
                  std::filesystem::path zipFilePath) {
  int errorCode = 0;
  zip_t* zipArchive = zip_open(zipFilePath.generic_u8string().c_str(),
                               ZIP_CREATE | ZIP_TRUNCATE, &errorCode);
  if (zipArchive) {
    CompressFile2Zip(unZipFilePath, unZipFilePath.filename().string().c_str(),
                     zipArchive);

    errorCode = zip_close(zipArchive);
    if (errorCode != 0) {
      zip_error_t zipError;
      zip_error_init_with_code(&zipError, errorCode);
      std::cerr << zip_error_strerror(&zipError) << std::endl;
      zip_error_fini(&zipError);
    }
  } else {
    zip_error_t zipError;
    zip_error_init_with_code(&zipError, errorCode);
    std::cerr << "Failed to open output file " << zipFilePath << ": "
              << zip_error_strerror(&zipError) << std::endl;
    zip_error_fini(&zipError);
  }
}

void CompressDirectory2Zip(std::filesystem::path rootDirectoryPath,
                           std::filesystem::path directoryPath,
                           zip_t* zipArchive) {
  if (rootDirectoryPath != directoryPath) {
    if (zip_dir_add(zipArchive,
                    std::filesystem::relative(directoryPath, rootDirectoryPath)
                        .generic_u8string()
                        .c_str(),
                    ZIP_FL_ENC_UTF_8) < 0) {
      std::cerr << "Failed to add directory " << directoryPath
                << " to zip: " << zip_strerror(zipArchive) << std::endl;
    }
  }

  for (const auto& entry : std::filesystem::directory_iterator(directoryPath)) {
    if (entry.is_regular_file()) {
      CompressFile2Zip(
          entry.path().generic_u8string(),
          std::filesystem::relative(entry.path(), rootDirectoryPath)
              .generic_u8string()
              .c_str(),
          zipArchive);
    } else if (entry.is_directory()) {
      CompressDirectory2Zip(rootDirectoryPath, entry.path().generic_u8string(),
                            zipArchive);
    }
  }
}

void CompressDirectory(std::filesystem::path directoryPath,
                       std::filesystem::path zipFilePath) {
  int errorCode = 0;
  zip_t* zipArchive = zip_open(zipFilePath.generic_u8string().c_str(),
                               ZIP_CREATE | ZIP_TRUNCATE, &errorCode);
  if (zipArchive) {
    CompressDirectory2Zip(directoryPath, directoryPath, zipArchive);

    errorCode = zip_close(zipArchive);
    if (errorCode != 0) {
      zip_error_t zipError;
      zip_error_init_with_code(&zipError, errorCode);
      std::cerr << zip_error_strerror(&zipError) << std::endl;
      zip_error_fini(&zipError);
    }
  } else {
    zip_error_t zipError;
    zip_error_init_with_code(&zipError, errorCode);
    std::cerr << "Failed to open output file " << zipFilePath << ": "
              << zip_error_strerror(&zipError) << std::endl;
    zip_error_fini(&zipError);
  }
}

int main() {
  //压缩文件
  // CompressFile("C:/Data/Builder/Demo/view.tmp",
  // "C:/Data/Builder/Demo/view.zip");

  //压缩文件夹
  CompressDirectory("C:/Data/Builder/Demo", "C:/Data/Builder/Demo.zip");

  return 0;
}

```

CMakeLists.txt的内容如下：



```
# 输出cmake版本提示
message(STATUS "The CMAKE_VERSION is ${CMAKE_VERSION}.")

# cmake的最低版本要求
cmake_minimum_required (VERSION 3.9)

# 工程名称、版本、语言
project (ZipTest VERSION 0.1 LANGUAGES CXX)

# cpp17支持
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 查找依赖库
find_package(libzip REQUIRED)

# 将源代码添加到此项目的可执行文件。
add_executable (${PROJECT_NAME} "main.cpp")

# 链接依赖库
target_link_libraries(${PROJECT_NAME} PRIVATE libzip::zip)

```

CMakePresets.json的内容如下：



```
{
  "version": 2,
  "configurePresets": [
    {
      "name": "linux-default",
      "displayName": "Linux Debug",
      "description": "面向适用于 Linux 的 Windows 子系统(WSL)或远程 Linux 系统。",
      "generator": "Ninja",
      "binaryDir": "${sourceDir}/out/build/${presetName}",
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "Debug",
        "CMAKE_INSTALL_PREFIX": "${sourceDir}/out/install/${presetName}"
      },
      "vendor": {
        "microsoft.com/VisualStudioSettings/CMake/1.0": { "hostOS": [ "Linux" ] },
        "microsoft.com/VisualStudioRemoteSettings/CMake/1.0": { "sourceDir": "$env{HOME}/.vs/$ms{projectDirName}" }
      }
    },
    {
      "name": "windows-default",
      "displayName": "Windows x64 Debug",
      "description": "面向具有 Visual Studio 开发环境的 Windows。",
      "generator": "Ninja",
      "binaryDir": "${sourceDir}/out/build/${presetName}",
      "architecture": {
        "value": "x64",
        "strategy": "external"
      },
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "Debug",
        "CMAKE_INSTALL_PREFIX": "${sourceDir}/out/install/${presetName}"
      },
      "vendor": { "microsoft.com/VisualStudioSettings/CMake/1.0": { "hostOS": [ "Windows" ] } }
    },
    {
      "name": "RelWithDebInfo",
      "displayName": "Windows x64 RelWithDebInfo Shared Library",
      "description": "面向具有 Visual Studio 开发环境的 Windows。",
      "generator": "Ninja",
      "binaryDir": "${sourceDir}/out/build/${presetName}",
      "architecture": {
        "value": "x64",
        "strategy": "external"
      },
      "cacheVariables": {
        "CMAKE_BUILD_TYPE": "RelWithDebInfo",
        "CMAKE_INSTALL_PREFIX": "${sourceDir}/out/install/${presetName}"
      },
      "vendor": { "microsoft.com/VisualStudioSettings/CMake/1.0": { "hostOS": [ "Windows" ] } }
    }
  ]
}

```

请务必注意，我们这里使用的是CMake比较推荐和比较新的目标链接机制来引入libzip库，关于这一点请务必复习上一篇博文的内容。这里要说的是如果`find_package(libzip REQUIRED)`失败，那么可能需要指定依赖库的安装目录，具体是在CMakePresets.json文件中的RelWithDebInfo配置中增加`CMAKE_PREFIX_PATH`，笔者这里使用的GISBasic环境变量指向的目录。至于libzip如何构建安装？可以参考本系列之前的博文。



```
{
    "name": "RelWithDebInfo",
    "displayName": "Windows x64 RelWithDebInfo Shared Library",
    "description": "面向具有 Visual Studio 开发环境的 Windows。",
    "generator": "Ninja",
    "binaryDir": "${sourceDir}/out/build/${presetName}",
    "architecture": {
        "value": "x64",
        "strategy": "external"
    },
    "cacheVariables": {
        "CMAKE_BUILD_TYPE": "RelWithDebInfo",
        "CMAKE_PREFIX_PATH": "$env{GISBasic}",
        "CMAKE_INSTALL_PREFIX": "${sourceDir}/out/install/${presetName}"
    },
    "vendor": {
        "microsoft.com/VisualStudioSettings/CMake/1.0": {
            "hostOS": [
                "Windows"
            ]
        }
    }
}

```

# 4\. 总结


好了，使用Visual Studio 2019进行CMake项目的开发的步骤和注意事项就是以上内容了。其实笔者也很想使用Visual Studio 2022甚至更新的版本来进行CMake项目的开发，不过受限于工作的环境没有进行升级。如果有试用的读者欢迎进行留言，看看与Visual Studio 2019对比有哪些区别或者提升。


