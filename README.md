# Generic Shovel bucket

In this repository you will find everything you need to know about creating custom bucket with appveyor support.

- [Files and helpers](#files-and-helpers)
    - [`bucket` Folder](#bucket-folder)
    - [`bin` Folder](#bin-folder)
    - [`Bucket.Tests.ps1` File](#buckettestsps1-file)
    - [`.vscode` Folder](#vscode-folder)
    - [`.github` Folder](#github-folder)
    - [`config files`](#config-files)
- [How to use and adopt this bucket](#how-to-use-and-adopt-this-bucket)

## Files and helpers

### `bucket` Folder

- All manifests belong here
- `.gitkeep` file could be removed when you push your first manifest

### `bin` Folder

If you need custom scripts you should create `bin` folder.

### `Bucket.Tests.ps1` File

- Test which are executed inside Appveyor pipeline
- Could be configured as `pre_commit` hook

### `.vscode` Folder

Contains all syntax highlighting, code formating, manifest creating tools you could use.

- Extensions
    - All extensions which will save your time while writing manifests are in recommended sections
    - You will be notified about installing them when you open project
- Settings
    - All settings are set to be compatible with Appveyor pipeline and upstream (official) repositories
        - No need to worry about formating restrictions between repositories.
- Code snippets
    - > Code snippets are templates that make it easier to enter repeating code patterns, such as loops or conditional-statements.
    - You could use workspace wide code snippets for speed up manifest creating
    - While editing json file write partitial name of snippet and press `tab`
    - Available Json snippets:
        - `app`
            - Create default manifest structure
        - `appArch`
            - Create default manifest structure with full acrchitecture
        - `arch`
            - Create only architecture property with 64bit and 32bit
        - `upAr`
            - Create autoupdate property with architecture

### `.github` Folder

GitHub repository configuration.

- `workflows` folder
    - [GitHub Actions](https://github.com/features/actions) configuration for automatic issue/PR/updates handling
    - Refer to [GithubActions repository](https://github.com/shovel-org/GithubActions) for more information
- `CODEOWNERS`
    - Pull requests will automatically request review for users defined in this file
- `PULL REQUEST TEMPLATE`
    - Prefilled pull request types with proper titles
- `ISSUE TEMPLATE`
    - The most used issue templates for users to select and prefilled with required information and labels

### `config files`

- `.appveyor.yml`
    - Definition of Appveyor CI pipeline
- `.editorconfig`
    - Universal configuration file, compatible with all types of editors
    - Defines how files should look
- `.gitattributes`
    - Simplifying line endings for git
    - No need to configure `auto.clrf` setting on each clone or new workspaces
- `Bucket.Tests.ps1`
    - Test which are executed inside Appveyor pipeline
    - Could be configured as `pre_commit` hook

## How to use and adopt this bucket

1. Click on `Use this template` to create new repository in your account with same files
1. Open project settings and **give your bucket new name**
1. Add proper description of repository
    - Information about what type of manifests could be found here
1. Add `shovel-bucket` tag for repository
    - If approved, your bucket could be part of <https://shovel.ash258.com> (Currently still Work-in-progress)
1. Enable appveyor CI/CD
    1. Register / Login to [Appveyor](https://ci.appveyor.com/login)
    1. Click `New Project`
    1. From Left Panel, choose your source control variant (Github)
    1. From Right Panel, choose repository with bucket and click `+ Add`
    1. 🎉 Project created and ready to build 🎉
    1. Get Badge URL
        1. Open Appveyor Project settings
        1. Navigate to Badges
        1. Copy `Branch Sample markdown code` snippet for further usage
            - Only master branch is better, since you can freely test in other branches and do not mystificate users
            - [You could use alternative styles](https://shields.io/category/build#styles)
1. Clone project into some folder
    - `git clone git@github.com:USER/REPO.git MyAwesomeBucket`
    - or
    - `git clone https://github.com/USER/REPO.git MyAwesomeBucket`
1. Open vscode with this clone
    - `code MyAwesomeBucket`
1. _[optional]_ Configure remote repository
    1. `git remote add 'upstream' 'https://github.com/Ash258/GenericBucket.git'`
    - This step will allow you to synchronize changes with this template repository
1. Create proper README.md
    1. [Open this README in the browser for reference](https://github.com/shovel-org/GenericBucket/tree/main/README.md)
    1. Open `README.template.md`
    1. Replace all `%%templatestring%%` with real and according values
        1. Replace appveyor status badge with yours
            - See: <https://appveyor.com/docs/status-badges/>
    1. Override this README with completed `README.template.md`
    1. Remove template `README.template.md`
1. Repository tweaks
    1. Open `.github\CODEOWNERS` and change `@Ash258` to desired GitHub username
    1. Actions
        1. Open each file in `.github\workflows` and change `youremail@email.com` with your email
        1. Visit <https://github.com/shovel-org/GithubActions> for more information
1. 🎉🎉 Everything set. High quality and automated bucket is ready for new users 🎉🎉

-   [scoop 教程](https://zhuanlan.zhihu.com/p/135278662)
-   file hash

https://scoop.sh/#/

```powershell
# 安装 scoop
set-executionpolicy remotesigned -scope currentuser
$env:SCOOP='D:\software\scoop'
[environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')
$env:SCOOP_GLOBAL='D:\software\globalScoopApps'
[environment]::setEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'Machine')
iwr -useb get.scoop.sh | iex
scoop install sudo
scoop install aria2
scoop checkup

# 使用
scoop list
scoop search
scoop update
scoop cache rm *
scoop uninstall
# 代理
scoop config proxy 127.0.1:7890
scoop config rm proxy

# 添加此仓库为存储桶  自己维护一个存储桶还是太麻烦了  后面只在这里放软件连接
scoop bucket add shirtiny https://github.com/Shirtiny/scoop_apps
# musicfox官方存储桶
scoop bucket add go-musicfox https://github.com/go-musicfox/go-musicfox.git 
# 其他桶
scoop bucket add extras
scoop bucket add nirsoft
scoop bucket add dorado https://github.com/h404bi/dorado
scoop bucket add Ash258 'https://github.com/Ash258/Scoop-Ash258.git'
scoop bucket add nerd-fonts
scoop bucket add java  # zulu
scoop bucket add versions

# 文件hash
certutil -hashfile file.exe SHA256

# terminal
scoop install ConEmu
scoop install oh-my-posh
scoop install Delugia-Nerd-Font-Complete
notepad $profile
```ps1
# oh-my-posh init pwsh --config "$(scoop prefix oh-my-posh)\themes\star.omp.json"
(@(& 'E:/software/scoop/apps/oh-my-posh/current/oh-my-posh.exe' init pwsh --config='E:\software\scoop\apps\oh-my-posh\current\themes\star.omp.json' --print) -join "`n") | Invoke-Expression
```

## 好用的软件
### macast  使用电脑接收发送自手机的视频、图片和音乐，支持主流视频音乐软件和其他任何符合DLNA协议的投屏软件
https://github.com/xfangfang/Macast/blob/main/README_ZH.md

### go-musicfox go-musicfox是用Go写的又一款网易云音乐命令行客户端
https://github.com/go-musicfox/go-musicfox

### TrafficMonitor 用于显示当前网速、CPU及内存利用率的桌面悬浮窗软件，并支持任务栏显示，支持更换皮肤。
https://github.com/zhongyang219/TrafficMonitor

### Folder-locker 给文件夹上锁 加密钥
https://github.com/Albert-W/Folder-locker

### yank note 一款强大可扩展的 Markdown 编辑器 可以在编写时运行代码
https://github.com/purocean/yn/blob/develop/README_ZH-CN.md

### SwitchHosts 是一个管理 hosts 文件的应用
https://github.com/oldj/SwitchHosts

### table plus 现代化的数据库GUI  正版需要购买
https://tableplus.com/

### Snipaste 是一个简单但强大的截图工具
https://zh.snipaste.com/

### termius SSH客户端、命令行工具 支持github学生包
https://termius.com/

### draw io 画流程图的
https://drawio-app.com/product/

### synfig 开源的动画制作工具 
https://github.com/synfig/synfig/

### potplayer 视频播放器
https://potplayer.tv/

### clash  强大又好看的代理工具  mac、win、安卓都有  ios上用choc，也是clash内核
https://github.com/Fndroid/clash_for_windows_pkg

### observablehq 在线 notebook
https://observablehq.com

### volta  node版本管理工具，类似nvm，但支持不同项目不同node版本
https://docs.volta.sh/guide/understanding#managing-your-project

### localsend 可以在同wifi下跨设备传输文件
https://github.com/localsend/localsend

### moonLight和sunshine串流
