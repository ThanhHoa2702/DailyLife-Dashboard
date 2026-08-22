# 🌟 LifeOS - Personal Management & Data Tracking Dashboard

**LifeOS** là một hệ thống quản lý cá nhân toàn diện hoạt động trực tiếp trên trình duyệt. Ứng dụng giúp số hóa các hoạt động hàng ngày thành một luồng dữ liệu có cấu trúc, cho phép theo dõi, trực quan hóa và xuất báo cáo tự động.

## Tính năng cốt lõi

*   **Quản lý Tài chính:** Theo dõi dòng tiền thu, chi, tích lũy bằng biểu đồ tự động cập nhật theo thời gian thực.
*   **Quản trị Mục tiêu & Thói quen:** Theo dõi tiến độ theo ngày/tháng với cơ sở dữ liệu lưu trữ bằng bộ nhớ thiết bị.
*   **Linh hoạt:** Chứa nhiều chức năng giúp tối ưu hóa việc quản lý mục tiêu ngắn hạn và dài hạn.
*   **Trích xuất báo cáo** Tổng hợp toàn bộ dữ liệu JSON trong tháng và biên dịch thành file Báo cáo Excel định dạng chuẩn.

---

## Hình ảnh về sản phẩm 

<img width="2540" height="1270" alt="image" src="https://github.com/user-attachments/assets/9e3b7d7e-d00c-4973-bf0e-768811eb9810" />

<img width="1466" height="1024" alt="image" src="https://github.com/user-attachments/assets/eab22c6e-3f36-4fe8-b4de-29ff91dae72d" />

<img width="1039" height="604" alt="image" src="https://github.com/user-attachments/assets/2fd6fa46-9dce-42a3-a2af-879664b7fa6e" />

---

## Mô tả

- Bảng tổng quan, mục tiêu hoàn thành và biểu đồ Tiến độ được tính dựa theo phần tab chứa 4 danh mục về mục tiêu đã đặt ra.

- Độ chăm chỉ sẽ dựa trên Habit Tracker ở mục thói quen và STREAK sẽ được tính dựa theo số ngày thực hiện liên tục. Nếu bị ngắt quãng sẽ không tính và trở về lại 0.

- Các tab quản lý có thể kéo thả, sắp xếp theo sở thích.

- Hiện tại chưa có chức năng đồng bộ trên nhiều thiết bị, nên chỉ sẽ có dữ liệu khi bạn truy cập vào 1 thiết bị. Nếu truy cập ứng dụng vào thiết bị khác thì sẽ không có thông tin.

---

## REVIEW
- Dự án học thuật chỉ mang tính chất tham khảo. Các bạn có thể sử dụng để xây dựng thói quen, tạo mục tiêu theo dõi cá nhân.
- Phần mềm không cần mạng trực tuyến vẫn có thể kết nối được, sử dụng bộ nhớ thiết bị truy cập của các bạn yên tâm về dữ liệu của mình.
- Mọi ý kiến, cập nhật, chỉnh sửa các bạn có thể góp ý để mình có thể cải thiện.

---

## Hướng dẫn đồng bộ

Phần đồng bộ có thể hơi rườm rà, nhưng đa phần chỉ là thao tác các bạn làm theo để có ứng dụng quản lý cho riêng mình nhé.

Bước 1: Tạo Máy chủ trên Google Drive
Máy chủ này sẽ làm nhiệm vụ lưu trữ và cập nhật dữ liệu, là cầu nối giữa các thiết bị:
1. Truy cập vào trang: script.google.com, đây là ứng dụng thuộc google
2. Đăng nhập bằng tài khoản Google
3. Bấm nút New Project ở góc trái
<img width="2552" height="1339" alt="image" src="https://github.com/user-attachments/assets/17722f46-a874-4a41-bd16-7f0f9a3fda8d" />

4. Đặt tên file các bạn muốn (ví dụ: LifeOS - Cloud API)
<img width="1271" height="1296" alt="image" src="https://github.com/user-attachments/assets/de742250-3473-4341-9875-37e22fcf395f" />

5. Xóa toàn bộ đoạn mã trong thư mục có sẵn, đưa toàn bộ đoạn mã dưới đây vào
```
const FILE_NAME = 'lifeos_data.json';

// Hàm xử lý yêu cầu lấy dữ liệu (Khởi động Web)
function doGet(e) {
  let data = readData();
  return ContentService.createTextOutput(data).setMimeType(ContentService.MimeType.JSON);
}

// Hàm xử lý yêu cầu lưu dữ liệu (Khi có thay đổi)
function doPost(e) {
  let data = e.parameter.data;
  if (data) {
    saveData(data);
    return ContentService.createTextOutput(JSON.stringify({status: 'success'}))
                         .setMimeType(ContentService.MimeType.JSON);
  }
  return ContentService.createTextOutput(JSON.stringify({status: 'error'}));
}

// Hàm đọc file từ Google Drive
function readData() {
  let files = DriveApp.getFilesByName(FILE_NAME);
  if (files.hasNext()) {
    return files.next().getBlob().getDataAsString();
  }
  return "{}"; // Trả về cục JSON rỗng nếu chưa có file
}

// Hàm lưu file đè lên Google Drive
function saveData(content) {
  let files = DriveApp.getFilesByName(FILE_NAME);
  if (files.hasNext()) {
    files.next().setContent(content);
  } else {
    DriveApp.createFile(FILE_NAME, content, MimeType.PLAIN_TEXT);
  }
}
```
<img width="1276" height="1341" alt="image" src="https://github.com/user-attachments/assets/cc088dd9-c8aa-425d-ae03-ee6e163e99d4" />

Bước 2: Tải link
Bước này hãy chú ý từng hướng dẫn và thao tác để không bị lỗi khiến làm lại từ đầu.
1. Ở trong trang script.google, ở góc trên cùng bên phải, bấm nút Triển khai (Deploy) -> Chọn tùy chọn triển khai mới (New deployment).
2. Ở bảng hiện ra, bấm nút biểu tượng bánh răng (Cài đặt) -> Chọn loại là Ứng dụng web (Web App).
<img width="1276" height="1327" alt="image" src="https://github.com/user-attachments/assets/b06fdf9d-ef19-4241-ad1d-57fec71d888a" />

4. Có 2 cấu hình chính:
  - Execute as: Chọn Tôi (Me).
  - Who has access: Chọn Anyone. Nếu không chọn sẽ bị báo lỗi.
5. Bấm Triển khai (Deploy). Google sẽ yêu cầu cấp quyền truy cập vào Drive (Authorize access). Cứ bấm tiếp tục và chọn tài khoản. Sau đó hiện ra các bạn hãy chọn "Nâng cao" -> Chọn Go to Untitled project (unsafe) và bấm "Cho phép". 
<img width="827" height="993" alt="image" src="https://github.com/user-attachments/assets/35a15cb6-cf33-4961-a927-a54b02b20857" />

6. Sau khi cấp quyền xong, các bạn sẽ được cung cấp một URL ứng dụng web. Hãy copy đường link URL đó.
<img width="918" height="745" alt="image" src="https://github.com/user-attachments/assets/89ede1de-08c4-422e-b465-85dbc5df926f" />

Bước 3: Gắn Link vào Code
Về phần code tôi đã tạo sẵn các bạn chỉ cần thao tác để tìm dòng code chính sau đó gắn link URL của google vào.

1. Các bạn nhấn vào file đã tải, nhấn chuột phải chọn mục Open With notepad.
<img width="1061" height="447" alt="image" src="https://github.com/user-attachments/assets/37562d09-ffe9-42cf-996a-78b324d7d458" />
2. Khi vào khung cửa sổ của notepad, các bạn nhấn tổ hợp phím CTRL + F để tìm kiếm dòng code.
<img width="2538" height="1383" alt="image" src="https://github.com/user-attachments/assets/33eaac98-fdb2-45ab-805d-58e92a0bb4ca" />
3. Copy phần code ``const CLOUD_API_URL`` vào phần tìm kiếm -> Sau đó gán URL đã copy trước đó vào dòng "Your_Google_Script_API_URL_HERE".
<img width="2559" height="1388" alt="image" src="https://github.com/user-attachments/assets/e707d904-baf8-41b6-8bcb-78756017039b" />

Chúc các bạn làm thành công. 


