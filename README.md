#  HỆ THỐNG THI TRẮC NGHIỆM TRỰC TUYẾN
# online-exam-ai-system
## 1. Giới thiệu
 **"Hệ thống Thi Trắc Nghiệm Trực Tuyến & Giám Sát AI (AI Proctoring System)"** là nền tảng web toàn diện được xây dựng nhằm giải quyết bài toán tổ chức thi cử trực tuyến một cách an toàn, minh bạch và chống gian lận hiệu quả. Dự án được thiết kế với giao diện hiện đại, trực quan theo bộ nhận diện Xanh dương đậm (#1E3A8A) và Trắng (#FFFFFF), đáp ứng trọn vẹn quy trình khảo thí cho cả hai phân hệ Giảng viên và Thí sinh. Về phía Giảng viên, hệ thống số hóa hoàn toàn từ khâu khởi tạo phòng thi, quản lý ngân hàng câu hỏi, điều phối danh sách lớp học phần cho đến phòng giám sát AI trực tiếp — cho phép theo dõi đồng thời 35–40 thí sinh, lọc nhanh các cảnh báo vi phạm và can thiệp kỷ luật tại chỗ (gửi nhắc nhở, tạm khóa bài làm hoặc đình chỉ thi), đồng thời tự động lưu trữ nhật ký vi phạm và thống kê phổ điểm báo cáo. Về phía Thí sinh, giao diện làm bài tích hợp đồng hồ đếm ngược, bảng điều hướng câu hỏi nhanh cùng luồng Webcam AI giám sát thời gian thực ở góc phải, giúp tự động nhận diện hành vi rời khỏi khung hình, quay mặt đi hướng khác hay chuyển tab trình duyệt để đảm bảo tính công bằng tuyệt đối cho kỳ thi.
## 2. Mục tiêu dự án
### 2.1. Đặt vấn đề & Thách thức thực tế
Trong kỷ nguyên giáo dục trực tuyến và đào tạo tín chỉ hiện nay, việc tổ chức các kỳ thi trắc nghiệm quy mô lớn gặp phải nhiều thách thức nghiêm trọng:
* **Áp lực giám sát:** Một giám thị phải quản lý hàng chục sinh viên qua màn hình, dẫn đến việc khó phát hiện kịp thời các hành vi gian lận tinh vi (như sử dụng tài liệu, trao đổi nhóm hoặc nhìn sang màn hình phụ).
* **Độ trễ phản hồi:** Các hệ thống thi truyền thống thiếu cơ chế cảnh báo hành vi bất thường thời gian thực, khiến việc xử lý vi phạm thường phải đợi đến khi hậu kiểm video ghi hình (mất rất nhiều thời gian).
* **Tải trọng máy chủ:** Việc xử lý luồng video giám sát trực tiếp của toàn bộ thí sinh trên máy chủ (Server-side rendering) dễ gây nghẽn băng thông và quá tải hệ thống.

### 2.2. Giải pháp và Kiến trúc hệ thống
Hệ thống **"Online Examination System with Real-time AI Proctoring"** được nghiên cứu và phát triển nhằm giải quyết triệt để các bài toán trên thông qua mô hình phân tán thông minh:
* **Edge Computing (Điện toán biên AI):** Tận dụng năng lực tính toán của trình duyệt phía client để chạy mô hình nhận diện khuôn mặt (`face-api.js`), giảm tải 90% băng thông cho máy chủ trung tâm.
* **Real-time Event-driven Architecture:** Ứng dụng công nghệ WebSocket (`Socket.IO`) để lập tức truyền tải các sự kiện vi phạm từ máy thí sinh lên màn hình điều khiển của giám thị ngay khi hành vi xảy ra.

### 2.3. Mục tiêu Cụ thể của Đồ án
* **Đối với Giảng viên:**
  * Số hóa toàn bộ quy trình từ khâu tạo phòng thi, quản lý ngân hàng câu hỏi, phân bổ danh sách lớp học phần đến việc chấm điểm và xuất báo cáo thống kê.
  * Cung cấp công cụ giám sát tập trung theo thời gian thực (Real-time Monitoring), cho phép theo dõi đồng thời hàng chục thí sinh trong cùng một ca thi và can thiệp xử lý vi phạm ngay lập tức (nhắc nhở, tạm khóa bài hoặc đình chỉ thi).
* **Đối với Thí sinh:**
  * Mang lại trải nghiệm làm bài thi trắc nghiệm trực tuyến thân thiện, trực quan với đồng hồ đếm ngược, bảng điều hướng câu hỏi thông minh và cơ chế tự động lưu trạng thái bài làm.
* **Đối với Hệ thống AI Proctoring:**
  * Ứng dụng thị giác máy tính (Computer Vision) và các sự kiện trình duyệt để tự động phát hiện, cảnh báo và ghi nhật ký các hành vi bất thường như: rời khỏi khung hình webcam, quay mặt đi hướng khác, xuất hiện nhiều khuôn mặt hoặc chuyển đổi tab trình duyệt.

## 3. Chức năng chính của hệ thống
* **Phân hệ Giảng viên (`Teacher Portal`):**
  * `teacher-dashboard.html`: Quản lý danh sách phòng thi, theo dõi trạng thái ca thi và điều hướng nhanh vào phòng giám sát.
  * `teacher-questions.html`: Quản lý, tìm kiếm và bổ sung ngân hàng câu hỏi trắc nghiệm theo từng môn học.
  * `teacher-classes.html`: Quản lý danh sách lớp học phần, sĩ số và xem chi tiết danh sách sinh viên qua hộp thoại Modal.
  * `teacher-monitor.html`: Phòng giám sát AI trực tiếp, hiển thị trạng thái của từng thí sinh, bộ lọc cảnh báo, xem luồng camera AI và thực hiện các thao tác kỷ luật.
  * `teacher-history.html`: Lưu trữ lịch sử các ca thi đã kết thúc kèm nhật ký (log) vi phạm chi tiết của từng sinh viên.
  * `teacher-reports.html`: Thống kê phổ điểm tự động (Mean, Median, tỷ lệ đạt), lọc kết quả theo từng lớp/môn thi và hỗ trợ xuất báo cáo.
* **Phân hệ Thí sinh & Module AI (`Student & AI Module`):**
  * `student-exam.html`: Giao diện làm bài thi trực tuyến tích hợp khung Webcam giám sát AI ở góc phải và cơ chế tự động khóa bài khi vi phạm quá số lần quy định (3 lần).
  * `ai-webcam.html`: Module kiểm thử độc lập luồng camera, khung quét nhận diện khuôn mặt (Bounding Box) và mô phỏng trạng thái cảnh báo AI.

## 4. Công nghệ sử dụng

| Thành phần | Công nghệ / Thư viện | Vai trò trong hệ thống |
| :--- | :--- | :--- |
| **Giao diện (Frontend)** | HTML5, CSS3 (Flexbox, Grid, CSS Variables) | Xây dựng bố cục chuẩn Responsive, đồng bộ bảng màu Trắng & Xanh dương đậm (`#1E3A8A`). |
| **Xử lý logic (Client)** | JavaScript (ES6+) | Xử lý tương tác động, render dữ liệu bảng, quản lý Modal, bộ đếm thời gian và trạng thái làm bài. |
| **AI & Thị giác máy tính** | `face-api.js`, HTML5 WebRTC (`getUserMedia`) | Truy cập luồng video từ Webcam, phát hiện khuôn mặt và phân tích hướng nhìn trực tiếp trên trình duyệt. |
| **Giám sát trình duyệt** | Page Visibility API (`visibilitychange`) | Phát hiện chính xác hành vi thí sinh chuyển tab hoặc rời khỏi cửa sổ làm bài thi. |
| **Kiến trúc kết nối** | RESTful API (`fetch` / Async-Await) | Tích hợp lớp dịch vụ gọi API sẵn sàng kết nối Backend Server, đi kèm cơ chế dữ liệu dự phòng (Fallback). |
## 5.Tổ chức Mã nguồn (Repository Structure)

```text
online-exam-ai-system/
├── client/                     # Phân hệ Giao diện người dùng (Frontend)
│   ├── public/models/          # Bộ trọng số mô hình AI (face-api.js weights)
│   ├── src/
│   │   ├── components/         # Các thành phần dùng chung (WebcamAI, AlertModal, Navbar)
│   │   ├── pages/              # Các trang chức năng (Login, StudentDashboard, ExamRoom, ProctorRoom...)
│   │   └── App.jsx             # Định tuyến luồng người dùng (Routing)
│   └── package.json
├── server/                     # Phân hệ Máy chủ (Backend API & WebSocket)
│   ├── src/
│   │   ├── config/             # Cấu hình kết nối MySQL
│   │   ├── controllers/        # Xử lý logic nghiệp vụ & chấm điểm
│   │   ├── routes/             # Định nghĩa các đường dẫn RESTful API
│   │   ├── sockets/            # Xử lý sự kiện cảnh báo thời gian thực (Socket.IO)
│   │   └── server.js           # Điểm khởi chạy máy chủ
│   ├── .env.example            # Mẫu cấu hình biến môi trường
│   └── package.json
├── database/                   # Tệp tin Cơ sở dữ liệu
│   └── schema.sql              # Mã lệnh SQL khởi tạo 7 bảng và dữ liệu mẫu
├── .gitignore                  # Loại trừ thư mục nặng/bảo mật (node_modules, .env)
└── README.md                   # Tài liệu đặc tả dự án
```
## Tài liệu dự án

| Tài liệu | Mô tả |
| :--- | :--- |
| [ai-webcam.html](ai-webcam.html) | Giao diện giám sát AI qua webcam |
| [index.html](index.html) | Trang chủ hệ thống thi trắc nghiệm |
| [student-exam.html](student-exam.html) | Màn hình làm bài thi chính thức của thí sinh |
| [student-home.html](student-home.html) | Trang tổng quan (Dashboard) của học sinh |
| [student-result.html](student-result.html) | Trang hiển thị kết quả và điểm thi |
| [style.css](style.css) | Tệp định dạng giao diện (CSS) chung cho toàn hệ thống |
| [teacher-classes.html](teacher-classes.html) | Quản lý danh sách lớp học của giảng viên |
| [teacher-dashboard.html](teacher-dashboard.html) | Trang tổng quan dành cho giảng viên |
| [teacher-history.html](teacher-history.html) | Lịch sử các kỳ thi và bài kiểm tra đã tạo |
| [teacher-monitor.html](teacher-monitor.html) | Màn hình giảng viên giám sát phòng thi trực tuyến |
| [teacher-questions.html](teacher-questions.html) | Quản lý ngân hàng câu hỏi trắc nghiệm |
| [teacher-reports.html](teacher-reports.html) | Thống kê và báo cáo kết quả thi của sinh viên |
* **Nhóm 6**
* Học phần: **Đồ Án 1**
* Trường Quốc tế- Đại học Quốc gia Hà Nội
