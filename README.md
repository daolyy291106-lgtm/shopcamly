# 💄 ROMAND Beauty Store

Website bán son Romand chính hãng (tham khảo mục son Romand tại thegioiskinfood.com), xây dựng bằng **Node.js + Express + SQLite**.

## ✨ Tính năng

**Khách hàng**
- Trang chủ hiển thị sản phẩm nổi bật + toàn bộ sản phẩm
- **Tìm kiếm** theo tên/dòng son, **lọc theo dòng son** (Juicy Lasting Tint, Zero Velvet Tint, Glasting Water Tint...), **sắp xếp** theo giá / bán chạy
- **Trang chi tiết sản phẩm**: mô tả, giá, **chọn màu son** (bảng màu chuẩn từng sản phẩm), chọn số lượng
- **Giỏ hàng**: thêm / sửa số lượng / xoá, tự tính phí ship (freeship từ 500.000đ)
- **Đặt hàng**: điền thông tin giao hàng + chọn phương thức thanh toán (COD / Chuyển khoản / MoMo)
- **Tra cứu đơn hàng**: theo mã đơn hoặc số điện thoại, xem trạng thái + timeline

**Quản trị** (`/admin/`)
- Thống kê doanh thu, số đơn, số sản phẩm
- Quản lý đơn hàng: xem, cập nhật trạng thái (chờ xác nhận → xác nhận → đang giao → đã giao / huỷ), trạng thái thanh toán, xoá
- Quản lý sản phẩm: thêm / sửa / xoá, quản lý màu son, giá, tồn kho
- Cài đặt: phí ship, ngưỡng freeship, thông tin shop, đổi mật khẩu admin

## 🚀 Cách chạy

**Cách 1 — Nhanh nhất:** double-click `start.bat` (tự mở trình duyệt).

**Cách 2 — Thủ công:**
```
cd D:\romand-shop
npm install
node server.js
```
Mở trình duyệt: http://localhost:3000

> Yêu cầu: Node.js >= 22.5 (đã cài sẵn trong lúc dựng). SQLite dùng module tích hợp sẵn của Node, **không cần cài database riêng**.

## 🔐 Tài khoản quản trị

| | |
|---|---|
| URL | http://localhost:3000/admin/ |
| Mật khẩu mặc định | `admin123` |

⚠️ Đổi mật khẩu ngay tại **Cài đặt** trước khi đưa lên mạng!

## 🗂 Cấu trúc thư mục

```
D:\romand-shop\
├── server.js              # Backend Express + API
├── lib\
│   ├── db.js              # Kết nối SQLite + truy vấn
│   ├── seed.js            # Script nạp dữ liệu mẫu (npm run seed)
│   └── seed-data.js       # Dữ liệu 15 sản phẩm / 100 màu son
├── scripts\gen-images.js  # Sinh ảnh sản phẩm SVG (npm run images)
├── data\romand.db         # Database SQLite (tự tạo khi chạy lần đầu)
└── public\                # Giao diện
    ├── index.html         # Trang chủ
    ├── product.html       # Chi tiết sản phẩm + chọn màu
    ├── cart.html          # Giỏ hàng
    ├── checkout.html      # Đặt hàng
    ├── track.html         # Tra cứu đơn hàng
    └── admin\             # Trang quản trị
```

## 🔄 Các lệnh hữu ích

```bash
npm start        # Chạy server
npm run seed     # Khôi phục lại dữ liệu sản phẩm mẫu (xoá đơn + sản phẩm đã sửa)
npm run images   # Sinh lại ảnh sản phẩm SVG
```

## 🌐 Đưa lên domain .io.vn

Website sẵn sàng đưa lên bất kỳ host/domain nào có đuôi `.io.vn` (ví dụ `romandstore.io.vn`):

1. **Đơn giản nhất — dùng VPS:** cài Node.js, copy thư mục `D:\romand-shop`, chạy `node server.js` (nên dùng PM2: `pm2 start server.js`), trỏ tên miền `.io.vn` về IP VPS và để reverse proxy (nginx) chuyển cổng 80 → 3000.
2. **Host tĩnh (Vercel/Netlify/Render):** Render có thể chạy Node app trực tiếp. Các nền tảng serverless cần bỏ SQLite file — đổi `lib/db.js` sang dịch vụ DB khác (MySQL/PostgreSQL).
3. Nhớ **đổi mật khẩu admin** và cập nhật **thông tin shop** ở trang Cài đặt.

## ⚠️ Lưu ý
- Giỏ hàng lưu ở trình duyệt (localStorage), đơn hàng lưu ở server (SQLite).
- Ảnh sản phẩm là SVG minh hoạ; có thể thay bằng ảnh thật bằng cách thay file trong `public\images\products\` (giữ tên file trùng `slug` sản phẩm) hoặc sửa sản phẩm ở trang quản trị.
