# VhalluploadkitForPaas
### 功能简介：

- 录播上传服务提供服务端上传视频生成录播支持，目前仅支持java语言

### 集成过程:
- 复制commons-codec-1.9.jar到工程lib目录下
- 复制commons-logging-1.2.jar到工程lib目录下
- 复制hamcrest-core-1.1.jar到工程lib目录下
- 复制httpclient-4.4.1.jar到工程lib目录下
- 复制httpcore-4.4.1.jar到工程lib目录下
- 复制jdom-1.1.jar到工程lib目录下
- 复制json-20170516.jar到工程lib目录下
- 复制vhalluploadkit_pass-1.0-release.jar到工程lib目录下

### 调用流程:
```
一、获取上传实例：VhallUploadKit
util = VhallUploadKit.getInstance();
二、使用在微吼PAAS平台注册应用时分配的APPID和SECRETKEY初始化
util.initData(APP_ID, SECRET_KEY);
三、初始化成功后，就可以上传视频生成录播
util.uploadAndBuildVideo(file, videoName,Callback, PutObjectProgressListener);
```

### API简介:

- 初始化
使用在微吼PAAS平台注册应用时分配的APPID和SECRETKEY初始化，重要！
```
 void initData(String APPID, String SecretKey)
```
- 是否可用
初始化成功后，VhallUploadKit才会处于可用状态，才能上传录播
```
 boolean isEnable()
```
- 上传视频并自动生成录播

```
/**
	 * 
	 * @param file
	 *            需要上传的文件
	 * @param videoName
	 *            录播名称
	 * @param callback
	 *            服务器回调
	 * @param listener
	 *            上传过程监听，返回当前上传状态及上传进度
	 * @return 文件对应OSS路径
	 */
 String uploadAndBuildVideo(File file, String videoName,Callback callback, ProgressListener listener)
```
- 停止上传
录播上传服务支持断点续传，上传过程中，本地会生成一个ucp文件，保存当前上传进度，如果上传操作被异常或手动中断，下次上传会自动定位到最后一次的上传位置继续上传。

```
/**
	 * 中断上传
	 *
	 * @param fileKey
	 *            上传返回的文件ID
	 * @return 是否成功
	 */
boolean stopUpload(String fileKey)
```
-取消上传
取消本次上传操作，取消操作会删除本地及服务器上传纪录和服务器上的文件碎片，重新从0开始上传
```
/**
	 * 取消上传
	 * 
	 * @param fileKey
	 *            上传返回的文件ID
	 * @return 是否成功
	 */
boolean abortUpload(String fileKey)
```
