# 🌟 LifeOS - Personal Management & Data Tracking Dashboard

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Vanilla JS](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E.svg?logo=javascript)
![ChartJS](https://img.shields.io/badge/Chart.js-FF6384.svg?logo=chartdotjs)
![Serverless](https://img.shields.io/badge/Backend-Google_Apps_Script-34A853.svg)

**LifeOS** là một hệ thống quản lý cá nhân toàn diện hoạt động trực tiếp trên trình duyệt. Ứng dụng giúp số hóa các hoạt động hàng ngày (Mục tiêu SMART, Thói quen, Tài chính) thành một luồng dữ liệu có cấu trúc, cho phép theo dõi, trực quan hóa và xuất báo cáo tự động.

> 📺 **[Xem Video Demo / Live Preview tại đây] (Chèn link video hoặc link web của bạn)**

---

## 📸 Ảnh chụp màn hình (Screenshots & GIFs)
*(Mẹo: Hãy chèn 2-3 ảnh GIF sinh động ghi lại cảnh bạn kéo thả mục tiêu, hoặc biểu đồ tài chính nhảy số khi thêm giao dịch. Hình động "ăn tiền" hơn hình tĩnh rất nhiều).*

<p align="center">
  <img src="link_anh_giao_dien_chinh.png" width="800" alt="Dashboard Preview">
</p>

---

## 🎯 Tính năng cốt lõi (Core Features)

*   **📊 Trực quan hóa dữ liệu Tài chính:** Theo dõi dòng tiền (Thu/Chi/Tích luỹ) bằng biểu đồ Chart.js tự động cập nhật theo thời gian thực.
*   **🛠 Quản trị Mục tiêu SMART & Thói quen:** Theo dõi tiến độ theo ngày/tháng với cơ sở dữ liệu lưu trữ tĩnh an toàn.
*   **🔄 Tương tác linh hoạt (Drag & Drop):** Sắp xếp mức độ ưu tiên công việc bằng thư viện SortableJS.
*   **📈 Trích xuất Báo cáo (Data Export):** Thuật toán tự động tổng hợp toàn bộ dữ liệu JSON trong tháng và biên dịch thành file Báo cáo Excel (`.xls`) định dạng chuẩn, tạo nguồn dữ liệu thô sạch sẽ cho việc phân tích chuyên sâu.

---

## 🧠 Kiến trúc Hệ thống & Luồng dữ liệu (Data Architecture)

Dự án được xây dựng theo hướng Serverless, tập trung vào tính toàn vẹn của dữ liệu và tối ưu hóa chi phí:

1.  **Client-side (Frontend):** Xây dựng hoàn toàn bằng HTML/CSS/JS thuần, không sử dụng framework nặng, giúp tối ưu tốc độ render DOM.
2.  **Cấu trúc Dữ liệu (JSON):** Dữ liệu được chuẩn hóa dưới dạng JSON Tree, phân tách theo từng key `YYYY-MM`.
3.  **Lưu trữ & Đồng bộ:** 
    *   Lưu trữ cục bộ với `LocalStorage` giúp ứng dụng hoạt động ngay cả khi Offline.
    *   Đồng bộ hóa lên đám mây thông qua API tự xây dựng bằng **Google Apps Script**, vượt qua rào cản CORS bằng phương thức `URLSearchParams`.

---

## 💡 Bài học rút ra (Lessons Learned)

Quá trình phát triển LifeOS đã giúp tôi hoàn thiện các kỹ năng thực tế:
*   **Quy hoạch dữ liệu:** Cách thiết kế cấu trúc Object hợp lý để dễ dàng lặp (iterate), tính toán tổng (aggregate) và vẽ biểu đồ.
*   **Xử lý sự kiện (Event Handling):** Quản lý trạng thái giao diện (UI State) mượt mà khi người dùng tương tác liên tục (kéo thả, chuyển tab).
*   **Giải quyết vấn đề (Problem Solving):** Tự viết thuật toán chuyển đổi cấu trúc dữ liệu JSON phức tạp thành bảng HTML thuần túy để xuất file Excel mà không phụ thuộc vào thư viện bên thứ ba.

---

## 💻 Cài đặt & Chạy cục bộ (Local Setup)

Dự án không yêu cầu cài đặt Node.js hay bất kỳ môi trường phức tạp nào.
1. Clone repository này về máy:
   ```bash
   git clone [https://github.com/TenCuaBan/LifeOS.git](https://github.com/TenCuaBan/LifeOS.git)
