### 1.安装java  
https://github.com/frekele/oracle-java/releases <BR/>
选择任意windows版本 <BR/>
jdk-8u212-windows-i586.exe <BR/>
添加系统变量：<BR/>
#### 2.1.    JAVA_HOME 
         C:\Program Files (x86)\Java\jdk1.8.0_212 <BR/>
#### 2.2.   Path
         %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin <BR/>
#### 2.3.  CLASSPATH 
         .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar <BR/>

### 2.安装Android Studio 
https://reactnative.cn/docs/getting-started/ <BR/>
添加系统变量 <BR/>
ANDROID_HOME <BR/>
C:\Users\admin\AppData\Local\Android\Sdk <BR/>
其中上述安装路径可以在Android Studio--》Configure--》SDK Manager--》Appearance & Behavior → System Settings → Android SDK→ Android SDK Location中找到 <BR/>
报错：Failed to install the following Android SDK packages as some licences have not been accepted.<BR/>
解决方案:进入Android SDK Manage 随便下载点东西 点击接受用户license <BR/>

### 3.创建RN项目
npx react-native init AwesomeProject <BR/>
cd AwesomeProject <BR/>
yarn android <BR/>
或者 <BR/>
yarn react-native run-android <BR/>
https://www.blyoo.com/4172.html  <BR/>

### React native开发的应用如何打包成APK IPA?
'react-native' 不是内部或外部命令，也不是可运行的程序或批处理文件。 <BR/>
npm install -g react-native-cli <BR/>
react-native log-android  新开窗口  运行命令 接收log <BR/>
https://blog.csdn.net/niuba123456/category_8956246.html <BR/>
在模拟器上Ctrl + M 进入开发者菜单 <BR/>
然后输入http://localhost:8081/debugger-ui/ 就可以看到console输出的内容了。 <BR/>
https://github.com/jd-smart-fe/shared/issues/3 <BR/>
在android studio 中的Logcat也可以看到console <BR/>

