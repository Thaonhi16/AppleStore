#  Apple Store – E-Commerce Web Application

> Dự án thực tế phục vụ học tập và kiểm thử phần mềm (Manual Testing Portfolio)

---

## Tổng quan dự án

**Apple Store** là ứng dụng web thương mại điện tử mô phỏng cửa hàng Apple, cho phép người dùng xem sản phẩm, thêm vào giỏ hàng, đặt hàng, đánh giá sản phẩm và quản lý tài khoản. Admin có thể quản lý sản phẩm, đơn hàng và tồn kho.

| Thông tin | Chi tiết |
|---|---|
| **Loại dự án** | Full-stack Web Application |
| **Frontend** | React 18, Vite, Ant Design |
| **Backend** | Node.js, Express 5, TypeScript |
| **Database** | MySQL (Prisma ORM) |
| **Auth** | JWT + Passport.js |
| **API Docs** | Swagger UI (`/api-docs`) |

---

## Kiến trúc hệ thống

```
AppleStore/
├── fe/          # React Frontend (Vite) → http://localhost:3000
└── be/          # Express Backend (TypeScript) → http://localhost:8888
    ├── src/
    │   ├── routes/      # API routes (auth, api, admin)
    │   ├── controllers/ # Business logic
    │   ├── services/    # Auth, business services
    │   ├── middleware/  # JWT, multer, passport
    │   └── config/      # Prisma client, seed data
    └── prisma/
        └── schema.prisma
```

---

## Cài đặt & Chạy dự án

### Yêu cầu

- Node.js >= 18
- MySQL đang chạy tại `localhost:3306`
- Database `ktpm` đã được tạo

### 1. Clone dự án

```bash
git clone https://github.com/<your-username>/apple-store.git
cd apple-store
```

### 2. Cài đặt Backend

```bash
cd be

# Tạo file .env từ mẫu
cp .env.example .env
# Chỉnh DATABASE_URL, PORT, JWT_SECRET trong .env

# Cài dependencies
npm install

# Đồng bộ schema với database
npx prisma db push

# Chạy server
npm run dev
# → http://localhost:8888
# → Swagger: http://localhost:8888/api-docs
```

### 3. Cài đặt Frontend

```bash
cd fe

# Cài dependencies
npm install

# Chạy dev server
npm run dev
# → http://localhost:3000
```

>  Backend sẽ tự động seed dữ liệu mẫu khi khởi động lần đầu.

---

## Tài khoản mẫu (sau khi seed)

| Role | Email | Password |
|------|-------|----------|
| Admin | admin@gmail.com | 123456 |
| Customer | test1@gmail.com | 123456 |
| Customer | test2@gmail.com | 123456 |

---

##  API Endpoints

| Module | Method | Endpoint | Auth |
|--------|--------|----------|------|
| **Auth** | POST | `/login` | ❌ |
| **Auth** | POST | `/register` | ❌ |
| **Products** | GET | `/api/products` | ❌ |
| **Products** | GET | `/api/product?page=1&limit=8` | ❌ |
| **Products** | GET | `/api/product/:id` | ❌ |
| **Category** | GET | `/api/category` | ❌ |
| **Cart** | GET | `/api/cart` | ✅ JWT |
| **Cart** | POST | `/api/add-product/:id` | ✅ JWT |
| **Cart** | DELETE | `/api/delete-product/:id` | ✅ JWT |
| **Order** | POST | `/api/place-order` | ✅ JWT |
| **Order** | GET | `/api/order-history` | ✅ JWT |
| **Wishlist** | GET | `/api/wishlist` | ✅ JWT |
| **Review** | POST | `/api/review` | ✅ JWT |
| **Profile** | PUT | `/api/profile` | ✅ JWT |
| **Admin** | GET | `/admin/products` | ✅ Admin |
| **Admin** | GET | `/admin/orders` | ✅ Admin |
| **Admin** | GET | `/admin/inventory` | ✅ Admin |

 Xem đầy đủ tại: `http://localhost:8888/api-docs`

---

## 📑 Tài liệu Kiểm thử (Testing Artifacts)

Toàn bộ kịch bản kiểm thử (Test Cases), Test Plan, và Bug Reports được mình tự thiết kế và quản lý chi tiết. Bạn có thể xem toàn bộ tài liệu gốc (Google Sheets/Docs) tại thư mục Drive dưới đây:

> 🔗 **[Xem toàn bộ tài liệu Test Cases & Bug Reports tại Google Drive](https://drive.google.com/drive/folders/19dBSAi9mgnooR2xhAWW3A7mCgzBhH-Az)**

*Lưu ý: Nếu có bất kỳ file nào yêu cầu quyền truy cập, vui lòng liên hệ mình qua Email cung cấp ở phần cuối.*

### 🎯 Phạm vi & Quy trình Kiểm thử (QA Workflow)
Dự án được thực hiện với quy trình kiểm thử bài bản, bao trọn vòng đời kiểm thử phần mềm (STLC):

1. **Test Planning & Analysis:** 
   - Phân tích yêu cầu nghiệp vụ và xây dựng **Test Plan**, **Test Checklist** chi tiết cho toàn bộ hệ thống.
2. **Test Design & Management:**
   - Thiết kế và quản lý Test Case bao phủ nhiều loại hình kiểm thử: **Functional, UI, Integration (API), Performance, Usability**.
3. **Test Execution (Manual & Tool-based):**
   - **Manual Testing:** Thực hiện kiểm thử chuyên sâu các chức năng cốt lõi (Login, Search, Cart, Checkout,...).
   - **API Testing:** Thực hiện kiểm thử tích hợp (Integration Test) và xác thực dữ liệu API. Toàn bộ kịch bản test API được tổ chức bài bản trên Postman:
     - 🌐 **[Live Postman Workspace](https://tothaonhi2004-1332985.postman.co/workspace/Nhy's-Workspace~a7621ec3-6438-4bf1-8c6a-ea74f1dba26a/collection/48912534-b810ea76-74b3-48a8-a221-d4eac2be7b32?action=share&source=copy-link&creator=48912534)**: Xem trực tiếp các request, params, và response mẫu trên web.
     - 📁 **Exported Collection**: File JSON đính kèm sẵn trong source code tại `be/postman/Apple-Store.postman_collection.json` (Hỗ trợ import nhanh chóng vào workspace cá nhân).
   - **Performance Testing:** Thực hiện kiểm thử hiệu năng cơ bản (đo lường Response Time, Load) bằng **JMeter**.
4. **Defect Management (Bug Tracking):**
   - Ghi nhận và theo dõi Bug trên hệ thống với đầy đủ thông tin chuẩn QA (Steps to reproduce, Expected/Actual result, Evidence, Priority/Severity).
5. **Test Reporting:**
   - Tổng hợp kết quả, đánh giá chất lượng phần mềm và viết **Test Report** nghiệm thu.

---

## 🧪 Test Cases Nổi Bật – Manual Testing

*(Bên dưới là một số Test Case nổi bật được trích xuất từ file Test Cases chính trong Google Drive)*

### 🔐 Module: Authentication

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC01 | Đăng nhập thành công | 1. Vào `/login`<br>2. Nhập email: `test1@gmail.com`, pass: `123456`<br>3. Click Login | Redirect về trang chủ, hiển thị tên user | High |
| TC02 | Đăng nhập sai mật khẩu | Nhập pass sai → Login | Hiển thị thông báo lỗi, không cho vào | High |
| TC03 | Đăng nhập email không tồn tại | Nhập email không có trong hệ thống | Hiển thị thông báo lỗi phù hợp | High |
| TC04 | Đăng nhập bỏ trống | Bỏ trống email hoặc password → Login | Hiển thị validation error | Medium |
| TC05 | Đăng ký tài khoản mới | Nhập đầy đủ thông tin hợp lệ → Register | Tạo tài khoản thành công, redirect | High |
| TC06 | Đăng ký email đã tồn tại | Nhập email đã dùng → Register | Thông báo email đã được sử dụng | High |
| TC07 | Đăng xuất | Click Logout | Xóa token, redirect về trang chủ | High |

###  Module: Sản phẩm

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC08 | Xem danh sách sản phẩm | Vào trang chủ | Hiển thị danh sách sản phẩm với ảnh, tên, giá | High |
| TC09 | Xem chi tiết sản phẩm | Click vào 1 sản phẩm | Hiển thị thông tin đầy đủ: mô tả, variant, giá, review | High |
| TC10 | Lọc sản phẩm theo category | Chọn "iPhone" từ menu | Chỉ hiển thị sản phẩm iPhone | Medium |
| TC11 | Phân trang sản phẩm | Scroll/click trang tiếp theo | Load đúng trang tiếp theo | Medium |
| TC12 | Chọn màu/dung lượng variant | Vào chi tiết SP → chọn biến thể | Giá cập nhật theo biến thể đã chọn | High |

###  Module: Giỏ hàng

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC13 | Thêm sản phẩm vào giỏ (chưa login) | Click "Add to Cart" khi chưa đăng nhập | Redirect về trang login | High |
| TC14 | Thêm sản phẩm vào giỏ (đã login) | Đăng nhập → Add to Cart | Số lượng giỏ hàng tăng lên | High |
| TC15 | Xem giỏ hàng | Click icon Cart | Hiển thị đúng sản phẩm và tổng tiền | High |
| TC16 | Xóa sản phẩm khỏi giỏ | Click nút xóa trong giỏ hàng | Sản phẩm bị xóa, tổng tiền cập nhật | High |
| TC17 | Thay đổi số lượng | Tăng/giảm quantity trong giỏ | Tổng tiền cập nhật tương ứng | High |

###  Module: Đặt hàng

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC18 | Đặt hàng thành công | Có hàng trong giỏ → Checkout → Nhập địa chỉ → Đặt hàng | Đơn hàng được tạo, giỏ hàng rỗng | High |
| TC19 | Checkout giỏ hàng trống | Vào /checkout khi chưa có sản phẩm | Redirect hoặc thông báo giỏ hàng trống | Medium |
| TC20 | Xem lịch sử đơn hàng | Vào Order History | Hiển thị danh sách các đơn hàng đã đặt | High |
| TC21 | Hủy đơn hàng PENDING | Vào Order History → Cancel | Đơn hàng chuyển sang trạng thái CANCELED | High |
| TC22 | Hủy đơn hàng COMPLETE | Thử cancel đơn đã hoàn thành | Không cho phép hủy, thông báo lỗi | Medium |

###  Module: Wishlist

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC23 | Thêm vào Wishlist | Đăng nhập → Click heart icon | Sản phẩm xuất hiện trong Wishlist | Medium |
| TC24 | Xóa khỏi Wishlist | Click lại heart icon / xóa trong Wishlist | Sản phẩm bị xóa | Medium |
| TC25 | Xóa tất cả Wishlist | Click "Clear All" | Wishlist trống | Low |

###  Module: Đánh giá sản phẩm

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC26 | Gửi đánh giá | Đăng nhập → Vào chi tiết SP → Chọn sao + nhập comment → Submit | Review hiển thị trong danh sách | Medium |
| TC27 | Xem đánh giá | Vào chi tiết sản phẩm | Hiển thị danh sách review với tên, sao, comment | Low |

###  Module: Tài khoản

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC28 | Cập nhật thông tin cá nhân | Vào Profile → Sửa tên/địa chỉ/phone → Save | Thông tin cập nhật thành công | Medium |
| TC29 | Upload avatar | Vào Profile → Chọn ảnh → Save | Avatar mới hiển thị | Low |

###  Module: Admin

| TC# | Test Case | Steps | Expected Result | Priority |
|-----|-----------|-------|-----------------|----------|
| TC30 | Đăng nhập Admin | Login với `admin@gmail.com` | Truy cập được trang Admin Dashboard | High |
| TC31 | Quản lý sản phẩm | Admin → Products | Xem danh sách, thêm/sửa/xóa sản phẩm | High |
| TC32 | Quản lý đơn hàng | Admin → Orders | Xem và cập nhật trạng thái đơn hàng | High |
| TC33 | Quản lý tồn kho | Admin → Inventory | Xem số lượng tồn kho từng variant | Medium |
| TC34 | Customer không vào được admin | Đăng nhập customer → vào `/admin` | Bị chặn, redirect hoặc 403 | High |

---

##  Bug Report Template

Khi phát hiện bug, ghi nhận theo format:

```
Bug ID: BUG-XXX
Tiêu đề: [Mô tả ngắn gọn]
Module: [Authentication / Cart / Order / ...]
Mức độ: Critical / High / Medium / Low
Môi trường: Browser, OS, version

Steps to Reproduce:
1. ...
2. ...
3. ...

Expected Result: [Kết quả mong muốn]
Actual Result:   [Kết quả thực tế]
Screenshot:      [Đính kèm nếu có]
```

---

##  Cấu trúc dữ liệu mẫu sau seed

- **4 categories**: MAC, IPHONE, IPAD, AIRPODS  
- **16 sản phẩm** với variants (màu sắc, dung lượng)  
- **4 users**: 1 admin + 3 customer  
- **Reviews** mẫu cho tất cả sản phẩm  
- **Wishlist** mẫu cho test1  

---

##  Tác giả

- **Tên**: Thảo Nhi
- **Email**: tothaonhi2004@gmail.com
- **Vị trí**: Tester / QA Engineer  

---

> 📝 Dự án này được xây dựng nhằm mục đích học tập và thực hành kiểm thử phần mềm thực tế.
