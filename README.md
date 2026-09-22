# Hướng Dẫn Thực Thi Từng Mục Tiêu Bài Lab (Walkthrough)

Tài liệu này hướng dẫn chi tiết cách thực thi từng mục tiêu trong kế hoạch bài lab WooCommerce.

---

## 🛠️ Bộ Tài Nguyên Đã Chuẩn Bị Sẵn

Trong thư mục `d:\Lab_WooCommerce`:
1. [docker-compose.yml](file:///d:/Lab_WooCommerce/docker-compose.yml): Cấu hình 4 container LEMP (Nginx, WordPress, MariaDB, phpMyAdmin).
2. [nginx/default.conf](file:///d:/Lab_WooCommerce/nginx/default.conf): File cấu hình Nginx URL rewrite.
3. [php/uploads.ini](file:///d:/Lab_WooCommerce/php/uploads.ini): Cấu hình RAM và upload limit cho PHP.

---

## 🚀 Hướng Dẫn Thực Hiện Từng Mục Tiêu

### Mục tiêu 1: Setup WordPress & WooCommerce
1. Mở PowerShell tại thư mục `d:\Lab_WooCommerce` và chạy lệnh:
   ```bash
   docker compose up -d
   ```
2. Mở trình duyệt truy cập: **[http://localhost:8080](http://localhost:8080)** để hoàn tất cài đặt WordPress:
   - Ngôn ngữ: English hoặc Tiếng Việt.
   - Điền thông tin website và tài khoản Admin.
3. Vào trang quản trị (`http://localhost:8080/wp-admin`):
   - Vào **Plugins** ➔ **Add New Plugin** ➔ Tìm và cài **WooCommerce** ➔ Bấm **Activate**.
   - Vào **Settings** ➔ **Permalinks** ➔ Chọn **Post name** ➔ Bấm **Save Changes** *(bắt buộc để không bị lỗi 404 REST API)*.

---

### Mục tiêu 2: Cài Đặt Flatsome Theme
1. Bạn chuẩn bị file `flatsome.zip` (hoặc thư mục theme `flatsome`).
2. Trong WP Admin:
   - Vào **Appearance** ➔ **Themes** ➔ **Add New Theme** ➔ **Upload Theme** ➔ Chọn file `flatsome.zip` ➔ Bấm **Install Now** ➔ **Activate**.
3. Chạy Flatsome Setup Wizard:
   - Tạo **Flatsome Child Theme**.
   - Cài các plugin mặc định đi kèm (UX Builder...).
   - Bấm hoàn tất để áp dụng giao diện.

---

### Mục tiêu 3: Cài Đặt Thông Tin Cửa Hàng, Vận Chuyển, Thanh Toán
1. **Thông tin cửa hàng & Tiền tệ:**
   - Vào **WooCommerce** ➔ **Settings** ➔ Tab **General**.
   - Điền Store Address (Địa chỉ, Thành phố, Quốc gia).
   - Mục **Currency options**: Chọn `Vietnamese đồng (đ)`.
2. **Khu vực vận chuyển (Shipping):**
   - Chuyển sang tab **Shipping** ➔ **Add shipping zone** (ví dụ: *Toàn quốc* hoặc *Nội thành*).
   - Bấm **Add shipping method**:
     - Thêm **Flat rate** (ví dụ: 30.000đ).
     - Thêm **Free shipping** (ví dụ: đơn hàng tối thiểu 500.000đ).
3. **Phương thức thanh toán (Payments):**
   - Chuyển sang tab **Payments**:
     - Bật **Cash on delivery (COD)** - Trả tiền mặt khi giao hàng.
     - Bật **Direct bank transfer (BACS)** - Chuyển khoản ngân hàng (điền tên ngân hàng, số tài khoản).

---

### Mục tiêu 4: Thêm Sản Phẩm Thủ Công (Manual)
1. Vào **Products** ➔ **Add New**.
2. **Thêm sản phẩm đơn giản (Simple Product):**
   - Product name: `Bàn di chuột Gaming RGB`
   - Regular price: `250000`
   - Inventory tab: SKU: `PAD-RGB-01`, bật *Manage stock?*, nhập Quantity: `50`.
   - Chọn Product Category, thêm ảnh sản phẩm (Product image).
   - Bấm **Publish**.
3. **Thêm sản phẩm biến thể (Variable Product):**
   - Đổi Product data sang **Variable product**.
   - Tab **Attributes**: Thêm thuộc tính `Size` (giá trị: `S | M | L`), tích chọn *Used for variations*.
   - Tab **Variations**: Bấm *Generate variations*, đặt giá riêng cho từng size (ví dụ Size S: 200k, Size M: 220k, Size L: 250k).
   - Bấm **Publish**.

---

### Mục tiêu 5: Import Sản Phẩm Bằng CSV
1. Vào **Products** ➔ **Import**.
2. Chọn file csv/txt cua thay đã chuẩn bị sẵn trong thư mục.
3. Bấm **Continue** ➔ Màn hình ánh xạ cột (Column mapping) hiện ra, WooCommerce sẽ tự động nhận diện tất cả các cột.
4. Bấm **Run the importer** và chờ hoàn tất.
5. Kiểm tra danh sách: Toàn bộ 5 sản phẩm với giá, hình ảnh và danh mục sẽ xuất hiện đầy đủ trong cửa hàng.

---

### Mục tiêu 6: Cập Nhật Số Lượng & Giá (Manual & Bulk Edit)
1. **Chỉnh sửa nhanh (Quick Edit):**
   - Vào danh sách **Products** ➔ rê chuột vào 1 sản phẩm bất kỳ ➔ bấm **Quick Edit**.
   - Thay đổi **Price** hoặc **Stock qty** ➔ Bấm **Update**.
2. **Chỉnh sửa hàng loạt (Bulk Edit):**
   - Tích chọn 3 sản phẩm trong bảng.
   - Tại ô *Bulk actions* ở góc trên bên trái, chọn **Edit** ➔ bấm **Apply**.
   - Thay đổi đồng loạt: ví dụ chọn mục *Sale* ➔ giảm giá 10%, hoặc đổi trạng thái *In stock*.
   - Bấm **Update**.

---

### Mục tiêu 7: Import Cập Nhật Số Lượng & Giá Bằng CSV
1. Vào **Products** ➔ **Import**.
2. Chọn file csv/txt.
3. **QUAN TRỌNG:** Tích vào ô **"Update existing products"** (Cập nhật các sản phẩm hiện có theo SKU).
4. Bấm **Continue** ➔ Ánh xạ cột `SKU`, `Regular price`, `Sale price`, `Stock`.
5. Bấm **Run the importer**.
6. Kết quả: Các sản phẩm có SKU tương ứng sẽ được cập nhật giá và tồn kho mới mà **không tạo thêm sản phẩm trùng lặp**.
7. 
