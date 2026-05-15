# Báo cáo nộp bài Lab W5 - Node.js Express on Lambda (BYOL)

**Người nộp:** Kiet (hoặc tên nhóm của bạn)
**Repository:** [https://github.com/kietoichoiDXD/xbrain-w5-node-express-lambda](https://github.com/kietoichoiDXD/xbrain-w5-node-express-lambda)
**Giảng viên chấm bài:** Anh Huỳnh Nghĩa (nghia.huynh@techxcorp.com)

---

## 🚀 1. Link API Gateway URL đã deploy
Dưới đây là link API Gateway gốc đã được deploy thành công lên môi trường AWS Lambda thông qua CloudFormation (`us-west-2`):
- **Root URL:** [https://rk1wybh4i4.execute-api.us-west-2.amazonaws.com](https://rk1wybh4i4.execute-api.us-west-2.amazonaws.com)
- **Test Endpoint (Hello):** [https://rk1wybh4i4.execute-api.us-west-2.amazonaws.com/api/hello/Lan](https://rk1wybh4i4.execute-api.us-west-2.amazonaws.com/api/hello/Lan)

Tất cả các endpoint (bao gồm POST `/api/echo`) đều hoạt động chính xác trả về đúng định dạng JSON chuẩn giống hệt lúc chạy Local.

---

## 📝 2. Chi tiết Chiến lược & Đo đạc Cold Start (Trích xuất từ NOTES.md)

### Chiến lược đã chọn: Strategy A — `serverless-http` adapter
**Lý do chọn chiến lược này:**
- **Minimal Code Change:** Chỉ cần thêm vỏn vẹn 3 dòng code khởi tạo vào một file mới là `lambda.js`.
- **Framework Pure (Giữ nguyên cấu trúc framework):** Các file hiện có như `app.js` và `server.js` được giữ nguyên hoàn toàn không bị tác động. Điều này giúp phần logic của Express.js tách biệt (decoupled) hoàn toàn khỏi các yếu tố đặc thù của AWS Lambda.
- **Tính ổn định (Robustness):** Thư viện `serverless-http` xử lý rất tốt các loại dữ liệu nhị phân (binary types), cookie và multi-value headers; qua đó giúp loại bỏ những lỗi đau đầu thường gặp khi phải biên dịch các event của API Gateway bằng tay (so với Strategy D).

### Cold Start Đo Được
- **Measured Init Duration (Thời gian khởi tạo):** `277.13 ms`
- **Phương pháp đo:** Đã lấy log thông qua việc kiểm tra dòng `REPORT` của first invocation ở AWS CloudWatch Logs (`/aws/lambda/byol-node-express-ExpressFunction-...`).

---

## 📂 3. Cấu trúc Source Code

- `lambda.js`: File Entrypoint mới dành riêng cho Lambda (Sử dụng `serverless-http`).
- `app.js` & `server.js`: Giữ nguyên bản gốc.
- `template.yaml`: Đã cấu hình Handler trỏ vào `lambda.js` và xử lý quyền triển khai.
- `NOTES.md`: Chứa các ghi chú gốc của quá trình thử nghiệm.

---
*Cảm ơn anh Nghĩa đã review bài tập này! Quền truy cập (Collaborator access) vào repo này đã được chia sẻ vào email nghia.huynh@techxcorp.com.*
