## 参数传递

通过在命令行中以-DparamKey=paramValue形式向gradle脚本中添加参数。

例：设置http/https代理：

```
gradlew -Dhttp.proxyHost=proxy.batechworks.com -Dhttp.proxyPort=8118 -Dhttps.proxyHost=proxy.batechworks.com -Dhttps.proxyPort=8118 clean app:assembleRelease
```

自定义参数设置，有时候需要在脚本中获取一些敏感数据，但这些数据不能hard code到代码中，需要通过参数传递到脚本

例：给apk签名

约定好keyAlias/keyPassword/storePassword参数key值，

```
gradlew -DkeyAlias=test -DkeyPassword=test123 -DstorePassword=test123 app:assembleRelease
```

在app的build.gradle中获取命令行中传入的值

```
def keystoreProperties = System.getProperties()
def keyAlias = keystoreProperties['keyAlias']
def keyPassword = keystoreProperties['keyPassword']
def storePassword = keystoreProperties['storePassword']
```

