# 📑 BÁO CÁO KẾT QUẢ LAB: NODE.JS EXPRESS ON LAMBDA (BYOL)

**Học viên:** [Tên của bạn]
**Ngày thực hiện:** 15/05/2026
**Khóa học:** AWS X-Brain Week 5
**Người hướng dẫn:** Anh Huỳnh Nghĩa (nghia.huynh@techxcorp.com)

---

## 🎯 1. Mục tiêu bài Lab
Chuyển đổi một ứng dụng Node.js Express truyền thống (chạy HTTP server) sang môi trường AWS Lambda (Serverless) với tiêu chí:
- **Thay đổi code ít nhất có thể (Minimum code changes).**
- **Giữ nguyên tính thuần khiết của framework (Framework Pure).**
- **Triển khai tự động hóa qua Infrastructure as Code (CloudFormation).**

---

## 🌐 2. Thông tin triển khai (Deployment Info)

| Thông tin | Chi tiết |
| :--- | :--- |
| **API Gateway URL** | [https://fpylwbd5wk.execute-api.us-west-2.amazonaws.com](https://fpylwbd5wk.execute-api.us-west-2.amazonaws.com) |
| **GitHub Repository** | [kietoichoiDXD/xbrain-w5-node-express-lambda](https://github.com/kietoichoiDXD/xbrain-w5-node-express-lambda) |
| **AWS Region** | `us-west-2` (Oregon) |
| **AWS Account ID** | `318662970982` |
| **Stack Name** | `byol-node-express-kietbe` |

---

## 🛠️ 3. Chiến lược triển khai (Strategy Selection)

### Chiến lược đã chọn: **Strategy A — `serverless-http` adapter**

#### **Lý do lựa chọn:**
1. **Chi phí thay đổi code cực thấp:** Chỉ mất 4 dòng code mới trong file `lambda.js`. Không cần sửa bất kỳ dòng nào trong core logic của `app.js`.
2. **Framework Pure:** Tách biệt hoàn toàn logic của ứng dụng (Express) và môi trường thực thi (Lambda). Ứng dụng vẫn có thể chạy local bằng `server.js` mà không cần quan tâm đến Lambda.
3. **Độ tin cậy cao:** Thư viện `serverless-http` là chuẩn công nghiệp, tự động xử lý các vấn đề phức tạp như Binary Data, Cookies, và Multi-value Headers mà không cần viết code xử lý sự kiện (Event Bridge) thủ công.

---

## 📊 4. Đo đạc hiệu năng (Performance Metrics)

Tôi đã thực hiện đo đạc Cold Start thông qua CloudWatch Logs (dòng `REPORT` của lần gọi đầu tiên):

- **Cold Start (Init Duration):** `336.78 ms`
- **Duration (Execution):** `~45 - 52 ms`
- **Memory Allocated:** `512 MB`
- **Max Memory Used:** `97 MB`

> **Nhận xét:** Thời gian khởi tạo dưới 400ms là mức lý tưởng cho một ứng dụng Express trung bình trên Lambda, đảm bảo trải nghiệm người dùng mượt mà ngay cả khi ứng dụng bị "đóng băng" trước đó.

---

## 🧪 5. Kết quả Smoke-test (Evidence)

Dưới đây là bằng chứng các endpoint hoạt động chính xác sau khi deploy:

### ✅ Endpoint: `/` (Root)
```json
{
  "ok": true,
  "runtime": "express",
  "message": "hello from your existing app"
}
```

### ✅ Endpoint: `/api/hello/Lan` (Path Parameters)
```json
{
  "greeting": "Hello, Lan!",
  "timestamp": "2026-05-15T10:08:33.926Z"
}
```

### ✅ Endpoint: `/api/echo` (POST Method)
**Body gửi lên:** `{"hi":"there"}`
**Kết quả:**
```json
{
  "echo": {
    "hi": "there"
  }
}
```

---

## 📁 6. Cấu trúc Source Code

- `lambda.js`: File entrypoint cho Lambda, sử dụng adapter để bọc (wrap) `app.js`.
- `app.js`: Giữ nguyên core logic của Express (Framework Pure).
- `template.yaml`: Định nghĩa hạ tầng (Lambda, API Gateway, IAM Role) chuẩn SAM/CloudFormation.
- `NOTES.md`: Ghi chú kỹ thuật nhanh về quá trình làm.

---
**Ghi chú nộp bài:** Tôi đã cấp quyền Collaborator cho anh Nghĩa (`nghia.huynh@techxcorp.com`) trên GitHub repository này.
