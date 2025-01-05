# dart_s3_storage

[中文文档](README-CN.md)

`dart_s3_storage` is a library that simplifies the integration and operation of object storage services compatible with the S3 protocol.

---

## ⚙️ Features

- 🌐 Supports object storage services compatible with the S3 protocol (e.g., AWS S3, Google Cloud Storage, Alibaba Cloud OSS, Cloudflare R2, MinIO, etc.)
- 📱 Simplifies storage operations for Dart and Flutter applications
- 🔌 Provides a consistent API interface for cross-platform storage integration
- ⬆️ Supports common operations like file upload, download, deletion, etc.

---

## 📥 Installation

Add the dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  s3_storage:
    git:
      url: https://github.com/halifox/dart_s3_storage
      ref: 1.0.7
```

---

## 🛠️ Usage

```dart
final s3_storage = S3Storage(
  endPoint: 's3.amazonaws.com',  // or '${Account_ID}.r2.cloudflarestorage.com'
  accessKey: 'Access Key ID',
  secretKey: 'Secret Access Key',
  signingType: SigningType.V4, // or SigningType.V2
);
```

**Upload an object to the bucket**

```dart
  String etag = await s3_storage.fPutObject('mybucket', 'myobject', 'path/to/file');
```

**Upload an object as a stream**

```dart
  String etag = await s3_storage.putObject(
    'mybucket',
    'myobject',
    Stream<Uint8List>.value(Uint8List(1024)),
    onProgress: (bytes) => print('$bytes uploaded'),
  );
```

**Retrieve an object from the bucket**

```dart
  final stream = await s3_storage.getObject('BUCKET-NAME', 'OBJECT-NAME');

  // Get object length
  print(stream.contentLength);

  // Write object data stream to a file
  await stream.pipe(File('output.txt').openWrite());
```

---

## API

### Bucket Operations
- **makeBucket**: Create a new bucket.
- **listBuckets**: List all buckets.
- **bucketExists**: Check if a specified bucket exists.
- **removeBucket**: Delete a bucket.
- **listObjects**: List objects in a bucket (traditional method).
- **listObjectsV2**: List objects in a bucket (V2, supports more features).
- **listIncompleteUploads**: List ongoing upload tasks.
- **listAllObjects**: List all objects in a bucket (including objects in subfolders).
- **listAllObjectsV2**: List all objects in a bucket (V2, supports more features).

### Object Operations
- **getObject**: Retrieve an object from a bucket.
- **getPartialObject**: Retrieve partial content of an object (supports chunked downloads).
- **fGetObject**: Retrieve an object from a bucket as a stream.
- **putObject**: Upload an object to a bucket.
- **fPutObject**: Upload an object to a bucket as a stream.
- **copyObject**: Copy an object from one location to another.
- **statObject**: Get object metadata (e.g., size, last modified time, etc.).
- **removeObject**: Delete an object from a bucket.
- **removeObjects**: Delete multiple objects from a bucket.

### Presigned Operations
- **presignedUrl**: Generate a temporary URL to access an object in a bucket.
- **presignedGetObject**: Generate a temporary URL to download an object from a bucket.
- **presignedPutObject**: Generate a temporary URL to upload an object to a bucket.
- **presignedPostPolicy**: Generate a temporary form upload URL, typically used for web form submissions.

### Bucket Policy & Notification Operations
- **getBucketNotification**: Get the bucket's notification configuration.
- **setBucketNotification**: Set the bucket's notification configuration for event-driven notifications (e.g., object uploads).
- **removeAllBucketNotification**: Remove all bucket notification configurations.
- **listenBucketNotification**: Listen for bucket notification events.
- **getBucketPolicy**: Get the bucket's access policy.
- **setBucketPolicy**: Set the bucket's access policy.
- **removeIncompleteUpload**: Remove incomplete upload tasks.

---

## 🤝 Contributing

We welcome all forms of community contributions!

Please read the [Contributing Guide (CONTRIBUTING.md)](CONTRIBUTING.md) to learn how to submit issues, request features, or contribute code.

---

## 📜 License

This library is modified from [s3_storage](https://pub.dev/packages/s3_storage), and the original author retains full copyright.

This project is licensed under the [LGPL-3.0 License](LICENSE).

All modified portions are still licensed under the [MIT License](MIT%20LICENSE) and include the original library's copyright and licensing information.

---

## 🙏 Acknowledgements

- [s3_storage](https://pub.dev/packages/s3_storage)

## 📢 Legal Disclaimer

This open-source project is for learning and communication purposes only. As it may involve patents or copyrights, please ensure you fully understand the relevant laws and regulations before use. **Do not use this tool for commercial purposes or distribute it in any form without authorization**.

All code and related content in this project is for personal technical learning and reference only. Any legal responsibility arising from its use is borne by the user.

Thank you for your understanding and support.