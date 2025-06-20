---
title: Seri Android Firebase Native
date: 2025-06-20 09:19:11
tags:
 - LinhNH
 - Firebase
 - Tổng quan
---

# Config Firebase cho Android Native

## Lời nói đầu

Chào mọi người, hôm nay nhân ngày đẹp trời mình sẽ gửi đến mọi người bài viết đầu tiên của mình trong Seri hướng dẫn cấu hình Firebase trong dự án Android Native. Chắc hẳn câu hỏi của nhiều người khi phát triển ứng dụng mobile là làm thế nào để có thể tạo 1 ứng dụng mà không cần phải biết backend và cần 1 server có thể lưu trữ dữ liệu của app. Firebase là một giải pháp tuyệt vời cho vấn đề này, nó có một nguồn tài nguyên khổng lồ và cung cấp nhiều dịch vụ hữu ích cho các ứng dụng Android. Trong bài viết này, mình sẽ hướng dẫn các bạn cách cấu hình Firebase cho dự án Android Native của bạn.

## Get Start

1. Đầu tiên bạn truy cập [Firebase Console](https://firebase.google.com/) và đăng nhập bằng tài khoản Google của bạn. Sau đó, bạn click vào **Get start in console** để truy cập vào bảng điều khiển Firebase. Nơi đây chứa các dự án firebase của bạn, nếu bạn chưa có dự án nào thì bạn click vào **Create a Firebase project** để tạo 1 dự án mới, bạn cần nhập tên dự án và tiếp tục.

![create_project_firebase](/css/images/linhnh/create_project_firebase.png "Create Project Firebase")

2. Sau khi tạo tên cho dự án, bạn chấp nhận các điều khoản và tiếp tục đi đến Configure Google Analytics. Ở đây bạn chọn **Default Account For Firebase** và tiếp tục. Kết quả như hình dưới đây.

![home_page](/css/images/linhnh/home_page.png "Home Page")

3. Đến đây bạn đã tạo thành công dự án firebase, tiếp theo chúng ta cần liên kết firebase với dự án Android Kotlin. Ở trang chủ firebase bạn click vào biểu tượng Android thêm ứng dụng Android tới Firebase.

![add_app_to_firebase](/css/images/linhnh/add_app_to_firebase.png "Add App to Firebase")

4. Bạn cần nhập **Package name** của ứng dụng Android của bạn. Package name này phải trùng với package name trong file `build.gradle` của ứng dụng Android tại dòng code như *namespace = "com.example.messageapp"*. Bạn có thể tìm thấy package name trong file `AndroidManifest.xml` hoặc trong file `build.gradle` (Module: app).

5. Tiếp theo bạn cần nhập key SHA-1 của ứng dụng. Để lấy được key này bạn cần chạy lệnh sau:
```
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
```
Sau đó trong terminal bạn tìm đến dòng SHA1: và copy key này vào ô SHA-1 key trong Firebase. Nếu bạn không có key này thì bạn có thể bỏ qua bước này và bấm **Register app** để liên kết , nhưng nếu bạn muốn sử dụng các dịch vụ như Firebase Authentication hoặc Firebase Dynamic Links thì bạn cần phải cung cấp key SHA-1.

6. Sau khi đăng kí xong bạn bấm tiếp vào **Download google-services.json** để tải về file cấu hình Firebase cho ứng dụng Android của bạn. File này chứa các thông tin cần thiết để kết nối ứng dụng Android với Firebase. Bạn cần đặt **google-services.json** vào vị trí thư mục `app/` trong dự án Android của bạn như mô tả bên dưới.

![download_google_service_json](/css/images/linhnh/download_google_service_json.png "Download Google Service Json")

7. Đến đây chúc mừng bạn đã cấu hình xong Firebase cho ứng dụng Android của bạn. Bây giờ bạn cần thêm các thư viện Firebase vào dự án Android của bạn. Bạn mở file `build.gradle` (Project) và thêm dòng code sau vào phần `dependencies`:

```
plugins {
  // ...

  // Add the dependency for the Google services Gradle plugin
  id("com.google.gms.google-services") version "4.4.2" apply false

}
```
Tiếp theo bạn mở file `build.gradle` (Module: app) và thêm code sau vào phần `dependencies`:

```
plugins {
  id("com.android.application")

  // Add the Google services Gradle plugin
  id("com.google.gms.google-services")

  ...
}

dependencies {
  // Import the Firebase BoM
  implementation(platform("com.google.firebase:firebase-bom:33.15.0"))


  // TODO: Add the dependencies for Firebase products you want to use
  // When using the BoM, don't specify versions in Firebase dependencies
  implementation("com.google.firebase:firebase-analytics")


  // Add the dependencies for any other desired Firebase products
  // https://firebase.google.com/docs/android/setup#available-libraries
}
```

## Tổng kết
Vậy là bạn đã hoàn thành việc cấu hình Firebase cho ứng dụng Android Native của mình. Bây giờ bạn có thể sử dụng các dịch vụ của Firebase như Firebase Realtime Database, Firebase Authentication, Firebase Cloud Messaging, v.v. để phát triển ứng dụng của mình một cách dễ dàng và hiệu quả. Nếu bạn muốn tìm hiểu thêm về các dịch vụ của Firebase, bạn có thể tham khảo tài liệu chính thức của Firebase tại [Firebase Documentation](https://firebase.google.com/docs). Bài viết sau mình sẽ nói đi sâu vào các dịch vụ của Firebase và cách sử dụng chúng trong ứng dụng Android của bạn. Hy vọng bài viết này sẽ giúp ích cho bạn trong việc phát triển ứng dụng Android của mình. Cảm ơn bạn đã đọc bài viết này!
