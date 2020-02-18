1.安装java
https://github.com/frekele/oracle-java/releases
选择任意windows版本
jdk-8u212-windows-i586.exe
添加系统变量：
2.1.    JAVA_HOME
         C:\Program Files (x86)\Java\jdk1.8.0_212
2.2.   Path
         %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin
2.3.  CLASSPATH
         .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar

2.安装Android Studio
https://reactnative.cn/docs/getting-started/
添加系统变量
ANDROID_HOME
C:\Users\admin\AppData\Local\Android\Sdk
其中上述安装路径可以在Android Studio--》Configure--》SDK Manager--》Appearance & Behavior → System Settings → Android SDK→ Android SDK Location中找到
报错：Failed to install the following Android SDK packages as some licences have not been accepted.
解决方案:进入Android SDK Manage 随便下载点东西 点击接受用户license

3.创建RN项目
npx react-native init AwesomeProject
cd AwesomeProject
yarn android
# 或者
yarn react-native run-android
https://www.blyoo.com/4172.html


React native开发的应用如何打包成APK IPA?
'react-native' 不是内部或外部命令，也不是可运行的程序或批处理文件。
npm install -g react-native-cli
react-native log-android  新开窗口  运行命令 接收log
https://blog.csdn.net/niuba123456/category_8956246.html
在模拟器上Ctrl + M 进入开发者菜单
然后输入http://localhost:8081/debugger-ui/ 就可以看到console输出的内容了。
https://github.com/jd-smart-fe/shared/issues/3
在android studio 中的Logcat也可以看到console

