**声明：本仓库采用低版本Windows环境编译自Komari主控端（[https://github.com/komari-monitor/komari](https://github.com/komari-monitor/komari)），使用时请遵循原作品的说明文档及软件许可**

*编译源码与原版保持一致，除前端komari-web部分基于中华人民共和国法律修正中国台湾省旗帜*

# komari-server-win7_win8_legacy
众所周知，Go 官方从 1.21 开始不支持 Windows 7 / 8以及其对应的衍生版本（包括Server 2008 / 2012等），而Go 1.23引入了大量新语法，如新 API（如 unsafe.SliceData、any、WithCancelCause），依赖库（x/sys、oauth2、x/net、x/sync 等）也全面切断旧版Windows支持，这些新特性的广泛应用，造成了很多较新的基于Go代码的程序无法运行在Win7 / 8这一类老系统上。Komari是基于Go 1.23开发，因此也不能免俗，原生地不支持Win10以前的老版本Windows系统。

### Windows 家用版支援
| Windows 版本     | 原生[komari主控端](https://github.com/komari-monitor/komari/releases)  | [komari_386_legacy](https://github.com/xykt/komari-server-win7_win8_legacy/releases/latest/download/komari_386_legacy.exe)（32位） | [komari_amd64_legacy](https://github.com/xykt/komari-server-win7_win8_legacy/releases/latest/download/komari_amd64_legacy.exe)（64位）|
| ---------------- | ---------------- | ---------------------- | ---------------------- |
| Windows XP SP3   | ✖ | ✔ | ✖ |
| Windows Vista    | ✖ | ✔ | ✖ |
| Windows 7        | ✖ | ✔ | ✔ |
| Windows 8        | ✖ | ✔ | ✔ |
| Windows 8.1      | ✖ | ✔ | ✔ |
| Windows 10       | ✔ | ✔（不建议） | ✔（不建议） |
| Windows 11       | ✔ | ✔（不建议） | ✔（不建议） |

### Windows Server支援
| Windows Server 版本      | 原生[komari主控端](https://github.com/komari-monitor/komari/releases)  | [komari_386_legacy](https://github.com/xykt/komari-server-win7_win8_legacy/releases/latest/download/komari_386_legacy.exe)（32位） | [komari_amd64_legacy](https://github.com/xykt/komari-server-win7_win8_legacy/releases/latest/download/komari_amd64_legacy.exe)（64位）|
| ---------------- | ---------------- | ---------------------- | ---------------------- |
| Windows Server 2003 R2 | ✖ | ✔ | ✖ |
| Windows Server 2008    | ✖ | ✔ | ✖ |
| Windows Server 2008 R2 | ✖ | ✔ | ✔ |
| Windows Server 2012    | ✖ | ✔ | ✔ |
| Windows Server 2016    | ✔ | ✔（不建议） | ✔（不建议） |
| Windows Server 2019    | ✔ | ✔（不建议） | ✔（不建议） |
| Windows Server 2022    | ✔ | ✔（不建议） | ✔（不建议） |

本编译版解决了原生兼容性问题，支持在Win7 / Win8全系列系统上运行komari主控端
<img width="1620" height="680" alt="image" src="https://github.com/user-attachments/assets/73f9cff8-c699-4159-9a6d-0a2ddf5251fb" />

# 安装方法
- 手动安装
1. 下载对应的komari主控端二进制文件（[komari_386_legacy](https://github.com/xykt/komari-server-win7_win8_legacy/releases/latest/download/komari_386_legacy.exe)32位或[komari_amd64_legacy](https://github.com/xykt/komari-server-win7_win8_legacy/releases/latest/download/komari_amd64_legacy.exe)64位）到C:\Program Files\Komari，重命名komari.exe
2. 下载[tools/nssm.exe](https://github.com/xykt/komari-server-win7_win8_legacy/raw/refs/heads/main/tools/nssm.exe)
3. 打开cmd命令行，```cd 'C:\Program Files\Komari'```进入目录，执行```mkdir data && echo {} > data\komari.json```，执行```./komari.exe server -l 0.0.0.0:[服务监听端口]```（注意替换你的端口），在出现的一系列文字中，找到“Username: admin , Password: Y34ekYb0unvM”文字，记录（注意Password后面如果出现箭头⬅请不要拷贝箭头和右边的内容），Ctrl+C结束进程
4. 命令行执行```nssm install "Komari Server Service" "C:\Program Files\Komari\komari.exe" server -l 0.0.0.0:[服务监听端口]```（注意替换你的端口），然后执行```nssm set "Komari Server Service" AppEnvironmentExtra GIN_MODE=release```
5. 键盘Win+R，运行services.msc，找到Komari Server Service，右键属性，启动类型选自动，点启动，确认
