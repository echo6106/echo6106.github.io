#androidkeystore配置
[百度](http://www.baidu.com)
**第一点**
    Android将debug.keystore改为和发布的key的sha1签名一样
在使用第三方sdk时，例如百度地图，需要使用签名的sha1的值。这个值可以在eclipse->windows->preferences->android->build里看到。
但这个值和发布key的sha1是不一样的。其实可以通过设置custom keystore的方式，使debug.keystore和发布的keystore的sha1值一样。
方法是：
1. 拷贝一份你的发布key
2. 修改这个key的别名为：androiddebugkey
3. 修改这个key的storepasswd 和 keypasswd为"android". （实际上debug.keystore这个默认生成的key的别名就是："androiddebugkey",两个口令是“android”）
在命令窗口执行的命令如下：
keytool -changealias -keystore mykeystore.keystore -alias [old alias] -destalias androiddebugkey 
keytool -keypasswd -keystore mykeystore.keystore -alias androiddebugkey 
keytool -storepasswd -keystore mykeystore.keystore

修改时，需要知道原来发布key的alias，可以通过以下命令查看alias：
keytool -list -v -keystore mykeystore.keystore

4. 设置eclipse->windows->preferences->android->build中的custom keystore为你这个改完口令的key文件，设置完成后，可以看到，这个key的sha1值和发布key的sha1值一样。

5. 拷贝这个key到同事的机器上，并设置custom keystore为这个key
keytool -list -v -keystore keystore.jks

