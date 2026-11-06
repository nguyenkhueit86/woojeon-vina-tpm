# Hệ thống Đi tuần hiện trường & Giám sát Stop Line (PRO-001) · IL-SUNG TECH

Hệ thống quản lý trực quan hiện trường sản xuất (Shop Floor Visual Management), kiểm tra checklist 5S / An toàn / Chất lượng, giám sát và phân tích dừng chuyền (Stop Line Monitoring) theo chuẩn nhà máy thông minh.

Được nâng cấp và tái cấu trúc hoàn toàn từ phiên bản cũ (1 file monolithic `index.html`) sang kiến trúc hiện đại **React 19 + Vite + Tailwind CSS + Lucide Icons + Supabase BaaS**.

---

## 🌟 Các tính năng & Cải tiến vượt trội

1. **Bản đồ hiện trường tương tác cao (Interactive Map with Zoom & Pan):**
   - Hỗ trợ phóng to, thu nhỏ (Zoom In/Out), kéo thả (Pan) mượt mà trên cả PC và thiết bị di động.
   - Ghim vị trí chính xác trên sơ đồ mặt bằng xưởng 17 Line và 19 khu vực ngoại vi.
   - Hiệu ứng nhấp nháy trực quan khi có cờ GẤP (🚨) hoặc lỗi quá hạn nặng (>8h).
   - Xem và duyệt Before - After: Ảnh vi phạm ban đầu đối soát trực quan với ảnh sau khi khắc phục.

2. **Đi tuần theo Checklist động & Quản lý điểm nóng:**
   - Checklist đồng bộ từ Supabase, phân nhóm tự động, đếm tỉ lệ Đạt / Không đạt thời gian thực.
   - Ràng buộc nghiêm ngặt: Mục "Không đạt" bắt buộc phải mô tả, chọn khu vực, ghim vị trí và chụp ảnh bằng chứng.
   - Báo nhanh sự cố khẩn cấp (Quick Report) cho mọi cán bộ nhân viên ngoài giờ đi tuần định kỳ.
   - Hỗ trợ chế độ ngoại tuyến (Offline Queue): Tự động lưu tạm vào máy khi mất mạng WiFi/4G trong xưởng và tự đồng bộ khi có mạng lại.

3. **Giám sát & Phân tích Stop Line thời gian thực:**
   - Bộ đếm phút dừng chuyền trực tiếp (Live Timer), phân cấp độ cảnh báo (Cấp 1 <5p, Cấp 2 <10p, Cấp 3 <15p, Cấp 4 ≥15p).
   - Lũy kế số phút dừng theo từng bộ phận (PRO, QC, MM, EQM, HR, INNO), tự động reset vào đúng mốc giao ca (08:01 và 20:01).
   - Thuật toán `sliceStop` cắt lát chính xác các sự cố vắt qua ranh giới ca để phân bổ đúng số phút cho Ca A và Ca C.
   - Nhận diện các sự cố nghi quên đóng (>12h) để không làm sai lệch số liệu thống kê.
   - Nhận xét & phân tích tự động bằng AI/Rules (Top line dừng nhiều nhất, tỷ trọng bộ phận chịu trách nhiệm, line lặp lại ≥3 lần).

4. **Bảng xếp hạng thi đua & Báo cáo quản trị:**
   - Bảng vinh danh bộ phận (🥇, 🥈, 🥉) tính theo điểm khắc phục đúng hạn, chỉ tiêu phát hiện lỗi và trách nhiệm trực tuần PLD.
   - Xuất file Excel (.xlsx) sự kiện dừng chuyền và số phút theo ca chỉ với 1 click.
   - Nút **"Chụp gửi Zalo"** kết xuất ảnh báo cáo sắc nét chuẩn mobile để chia sẻ tức thì lên nhóm Zalo nhà máy.

5. **Phân quyền người dùng & Cấu hình hệ thống:**
   - Hỗ trợ các vai trò: `leader`, `manager`, `group_leader`, `admin`.
   - Quản lý người dùng, đổi mã PIN, gán Part phụ trách.
   - Nhập / Xuất danh mục Checklist từ file Excel.
   - Cài đặt ngưỡng cảnh báo và nội dung banner thông điệp tuần tra.

---

## 📁 Cấu trúc thư mục dự án

```
Audit_Hientruong/
├── public/                     # Ảnh tĩnh (layout.png, factory.jpg)
├── src/
│   ├── constants/
│   │   └── zones.js            # Tọa độ 17 Line và 19 khu vực, mã màu bộ phận
│   ├── services/
│   │   └── supabase.js         # Kết nối Supabase, RPC helper, nén & upload ảnh
│   ├── utils/
│   │   ├── scoring.js          # Logic tính điểm SLA, phân chia ca 08:01/20:01, sliceStop
│   │   └── offlineQueue.js     # Lưu trữ hàng đợi ngoại tuyến khi mất sóng
│   ├── components/
│   │   ├── Header.jsx          # Thanh điều hướng trên cùng, trạng thái mạng, user badge
│   │   ├── InteractiveMap.jsx  # Bản đồ nhà máy Zoom/Pan, danh sách cờ, modal duyệt Before-After
│   │   ├── FlagPositionModal.jsx# Modal ghim tọa độ chính xác trên canvas
│   │   ├── WalkthroughForm.jsx # Phiếu đi tuần checklist, bộ đếm Đạt/Không đạt
│   │   ├── QuickReport.jsx     # Báo nhanh điểm nóng, cờ gấp
│   │   ├── StopLineView.jsx    # Giám sát dừng chuyền thời gian thực
│   │   ├── StopReportView.jsx  # Báo cáo phân tích Stop Line, biểu đồ ca, xuất Excel
│   │   ├── ReportView.jsx      # Báo cáo tổng hợp, xếp hạng thi đua bộ phận
│   │   ├── SettingsView.jsx    # Cấu hình ngưỡng, checklist, quản lý tài khoản
│   │   └── LoginModal.jsx      # Đăng nhập bằng tên & mã PIN, chế độ Khách
│   ├── App.jsx                 # Router chính điều hướng các tab
│   ├── main.jsx                # Entry point React 19
│   └── index.css               # Tailwind CSS v4 & custom animations
├── index.html                  # HTML template Vite
├── vite.config.js              # Cấu hình Vite & Tailwind plugin
├── package.json
└── README.md
```

---

## 🚀 Hướng dẫn cài đặt & Chạy ứng dụng

### 1. Cài đặt môi trường (Yêu cầu Node.js v18+)
```bash
# Cài đặt thư viện dependencies
npm install
```

### 2. Chạy môi trường phát triển (Development)
```bash
npm run dev
```
Trình duyệt sẽ tự động mở tại địa chỉ `http://localhost:3000`.

### 3. Đóng gói cho Production (Build)
```bash
npm run build
```
Toàn bộ mã nguồn sẽ được biên dịch và tối ưu vào thư mục `dist/`. Thư mục này sẵn sàng để triển khai lên bất kỳ Web Server nào (Nginx, Apache, IIS, GitHub Pages, Vercel, Netlify).

### 4. Triển khai lên GitHub Pages
Copy toàn bộ các file trong thư mục `dist/` vào nhánh `gh-pages` hoặc thư mục gốc repo GitHub của bạn để chạy dưới dạng GitHub Pages.
