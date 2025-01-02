# dart_s3_storage

`dart_s3_storage` 是一个简化 S3 协议兼容的对象存储服务集成与操作的库。

---

## ⚙️ 功能

- 🌐 支持兼容 S3 协议的对象存储服务（如 AWS S3、Google Cloud Storage、阿里云 OSS、Cloudflare R2、MinIO 等）
- 📱 简化了 Dart 与 Flutter 应用的存储操作
- 🔌 提供一致的 API 接口，便于跨平台存储集成
- ⬆️ 支持文件上传、下载、删除等常见操作

---

## 📥 安装

在 `pubspec.yaml` 文件中添加依赖：

```yaml
dependencies:
  s3_storage:
    git:
      url: https://github.com/halifox/dart_s3_storage
      ref: 1.0.7

```

---

## 🛠️ 使用方法

```dart
final s3_storage = S3Storage(
  endPoint: 's3.amazonaws.com',  //或 '${Account_ID}.r2.cloudflarestorage.com'
  accessKey: 'Access Key ID',
  secretKey: 'Secret Access Key',
  signingType: SigningType.V4, // 或 SigningType.V2
);
```

**向存储桶上传一个对象**

```dart
  String etag = await s3_storage.fPutObject('mybucket', 'myobject', 'path/to/file');
```

**以流式方式上传对象**

```dart
  String etag = await s3_storage.putObject(
    'mybucket',
    'myobject',
    Stream<Uint8List>.value(Uint8List(1024)),
    onProgress: (bytes) => print('$bytes uploaded'),
  );
```

**获取存储桶中的一个对象**

```dart
  final stream = await s3_storage.getObject('BUCKET-NAME', 'OBJECT-NAME');

  // Get object length
  print(stream.contentLength);

  // Write object data stream to file
  await stream.pipe(File('output.txt').openWrite());
```

---

## API

### Bucket Operations
- **makeBucket**：创建一个新的存储桶。
- **listBuckets**：列出所有存储桶。
- **bucketExists**：检查指定的存储桶是否存在。
- **removeBucket**：删除一个存储桶。
- **listObjects**：列出存储桶中的对象（传统方式）。
- **listObjectsV2**：列出存储桶中的对象（V2版本，支持更多功能）。
- **listIncompleteUploads**：列出正在进行的上传任务。
- **listAllObjects**：列出存储桶中的所有对象（包括子文件夹中的对象）。
- **listAllObjectsV2**：列出存储桶中的所有对象（V2版本，支持更多功能）。

### Object Operations
- **getObject**：获取存储桶中的一个对象。
- **getPartialObject**：获取存储桶中对象的部分内容（支持分块下载）。
- **fGetObject**：以流式方式获取存储桶中的一个对象。
- **putObject**：向存储桶上传一个对象。
- **fPutObject**：以流式方式上传对象。
- **copyObject**：将一个对象从一个位置复制到另一个位置。
- **statObject**：获取对象的元数据（如大小、最后修改时间等）。
- **removeObject**：删除存储桶中的一个对象。
- **removeObjects**：删除存储桶中的多个对象。

### Presigned Operations
- **presignedUrl**：生成一个临时的 URL，用于访问存储桶中的对象。
- **presignedGetObject**：生成一个临时 URL，用于下载存储桶中的对象。
- **presignedPutObject**：生成一个临时 URL，用于上传对象到存储桶。
- **presignedPostPolicy**：生成一个临时的表单上传 URL，通常用于 Web 表单提交。

### Bucket Policy & Notification Operations
- **getBucketNotification**：获取存储桶的通知配置。
- **setBucketNotification**：设置存储桶的通知配置，用于事件触发通知（如对象上传）。
- **removeAllBucketNotification**：删除存储桶的所有通知配置。
- **listenBucketNotification**：监听存储桶的通知事件。
- **getBucketPolicy**：获取存储桶的访问策略。
- **setBucketPolicy**：设置存储桶的访问策略。
- **removeIncompleteUpload**：移除未完成的上传任务。

---

## 🤝 贡献

我们欢迎任何形式的社区贡献！  

请阅读 [贡献指南 (CONTRIBUTING.md)](CONTRIBUTING.md)，了解如何提交 Issue、请求功能或贡献代码。

---

## 📜 许可证

该库基于 [s3_storage](https://pub.dev/packages/s3_storage) 修改而来，原作者保留完整版权。

本项目遵循 [LGPL-3.0 License](LICENSE)。

所有修改过的部分仍然遵循 [MIT License](MIT%20LICENSE)，并且包含原始库的版权声明和许可声明。

---

## 🙏 致谢

- [s3_storage](https://pub.dev/packages/s3_storage)

## 📢 法律声明

本开源项目仅供学习和交流用途。由于可能涉及专利或版权相关内容，请在使用前确保已充分理解相关法律法规。未经授权，**请勿将本工具用于商业用途或进行任何形式的传播**。

本项目的所有代码和相关内容仅供个人技术学习与参考，任何使用产生的法律责任由使用者自行承担。

感谢您的理解与支持。