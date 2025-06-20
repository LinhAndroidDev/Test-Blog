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


**Các thư viện phổ biến**
Có thể các bạn đã dùng nhiều thư viện nhưng có thể chưa để ý nó nằm trong Jetpack libraries. Dưới đây là một số thư viện mà chúng ta hay dùng.
- **Navigation** : Xây dựng và lập cấu trúc cho giao diện người dùng trong ứng dụng, xử lý deep-link và di chuyển giữa các màn hình.
- **Room** : Tạo mới, lưu trữ và quản lý dữ liệu được hỗ trợ bởi SQLite database.
- **Databinding** : Cái này chắc mọi người quá quen rồi. Thư viện dùng để liên kết các thành phần UI với data trong app bằng định dạng khai báo (hiểu nôm na là bạn sẽ không cần phải dung findViewById nữa).
- **Hilt** : Mở rộng chức năng Dagger Hilt để sử dụng kĩ thuật Dependency Injection đơn giản hơn (Sử dụng khá đơn giản, mọi người nên thử).
- **Activity(androidx.activity)**: [Activity](https://developer.android.com/jetpack/androidx/releases/activity?_gl=1*pux1ac*_up*MQ..&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds)
- **Appcompat(androidx.appcompat)** : [AppCompat](https://developer.android.com/jetpack/androidx/releases/appcompat?_gl=1*1h95g3h*_up*MQ..&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds)
- **AppSearch**: [AppSearch](https://developer.android.com/jetpack/androidx/releases/appsearch?_gl=1*1h95g3h*_up*MQ..&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds)
- **Camera**: [Camera](https://developer.android.com/jetpack/androidx/releases/camera?_gl=1*1h95g3h*_up*MQ..&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds)
- **Compose**: [Compose](https://developer.android.com/jetpack/androidx/releases/compose?_gl=1*m8tg1v*_up*MQ..&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds)
- **Fragment**: [Fragment](https://developer.android.com/jetpack/androidx/releases/fragment?_gl=1*m8tg1v*_up*MQ..&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds)
- **Lifecycle**: [Lifecycle](https://developer.android.com/jetpack/androidx/releases/lifecycle?_gl=1*1fwyy68*_up*MQ..&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds)

Còn mấy cái nữa cơ nhưng luời liệt kê quá, bạn có thể vào [link](https://developer.android.com/jetpack?gad_source=1&gclid=Cj0KCQiA0MG5BhD1ARIsAEcZtwR0PQaFlH50BXwBvWZwvNhXobfh78kks9Z6tO1uWRERW9ttkIhxZB8aAnsVEALw_wcB&gclsrc=aw.ds#:~:text=Read%20testimonials-,Jetpack%20libraries,-Explore%20all%20libraries) này để xem. Tôi học mót ở đây ra hết ấy mà :V.
**Các bạn chút ý nhé Compose chính là chủ đề chính ở các bài viết tiếp của mình nhé.**

Một sốt UI code bằng Jetpack Compose
![](https://miro.medium.com/v2/resize:fit:474/1*OnmTLPcraJ0kfnmRx1oSPg.gif)
![](https://raw.githubusercontent.com/android/compose-samples/refs/heads/main/readme/screenshots/Jetsnack.png)
![](https://raw.githubusercontent.com/android/compose-samples/refs/heads/main/readme/screenshots/Jetchat.png)
![](https://raw.githubusercontent.com/android/compose-samples/refs/heads/main/readme/screenshots/Jetcaster.png)
![](https://raw.githubusercontent.com/android/compose-samples/refs/heads/main/readme/screenshots/JetNews.png)
**Kết bài**
Bài giới thiệu của mình đến đây là kết thúc tuy có ngắn nhưng vẫn mong các bạn nắm qua một chút về **Android dẹt pạch**. Bài viết sau chúng ta sẽ đi chi tiết hơn về Jetpack Compose nhé. Làm thế nào để code UI bằng Jetpack compose, kết hợp việc code UI và lấy data từ api để hiển thị lên... Hẹn gặp các bạn ở bài viết sau nhé. 
