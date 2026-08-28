## 环境配置

### 必备的环境/工具

- #### java、node

- #### 模拟器

- https://developer.android.com/studio?hl=zh-cn#command-line-tools-only 里面的 commandlinetools-win-15859902_latest.zip 环境

## 下载 appium

> ```cmd
> C:\Users\86172>npm install -g appium
> ```

## 下载 Android 驱动

> ```cmd
> appium driver install uiautomator2
> ```

## 下载 appium SDK 组件

> ```cmd
> D:\Android\Sdk\cmdline-tools\latest\bin\sdkmanager.bat "platform-tools"	# platform-tools
> 
> D:\Android\Sdk\cmdline-tools\latest\bin\sdkmanager.bat "platforms;android-35"
> 
> D:\Android\Sdk\cmdline-tools\latest\bin\sdkmanager.bat "build-tools;35.0.0"
> ```
>
> 

## venv 虚拟环境中下载依赖

> ```powershell
> pip install Appium-Python-Client pytest
> 
> pip install requests allure-pytest
> ```

## 启动 Appium Server，跑用例

> ```cmd
> appium
> 
> 可以跑用例了
> ```
>

## 整体的 workflow

> pytest
>   ↓
> Appium-Python-Client
>   ↓
> Appium Server（http://127.0.0.1:4723）
>   ↓
> UiAutomator2
>   ↓
> D:\Android\Sdk\platform-tools\adb.exe
>   ↓
> 127.0.0.1:5555
>   ↓
> 雷电模拟器
>   ↓
> com.sohu.newsclient
>   ↓
> 操作

## 获取 App 的包、activity

> 例如：
>
> ```cmd
> options.app_package = "com.sohu.newsclient"
> options.app_activity = (
>      "com.sohu.newsclient.boot.activity.SplashActivity"
>  )
> ```
>
> 1. 启动模拟器，启动app
> 2. 获取 package：adb shell dumpsys window | findstr mCurrentFocus
>
>    ```cmd
>    C:\Users\86172>adb shell dumpsys window | findstr mCurrentFocus
>      mCurrentFocus=Window{5031286 u0 com.sohu.newsclient/com.sohu.newsclient.boot.activity.SplashActivity}
>    ```
> 3. 获取 activity：adb shell dumpsys activity activities | findstr mResumedActivity