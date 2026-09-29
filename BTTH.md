### Phần 1 — Xác định Entity / Attribute / Khóa chính

| Entity | Attribute cần lưu | Khóa chính (PK) |
|---|---|---|
| **LOP_TAP** | MaLop, TenLop, HocPhi | MaLop |
| **HOI_VIEN** | MaHoiVien (hoặc SoDienThoai), TenHoiVien, SoDienThoai | MaHoiVien (hoặc SoDienThoai) |
| **HUAN_LUYEN_VIEN** | MaHLV, TenHLV | MaHLV |

---

### Phần 2 — Xác định quan hệ và Khóa ngoại

| Cặp Entity | Loại quan hệ | Khóa ngoại đặt ở Entity nào (nếu N-N thì nêu tên bảng trung gian) |
|---|---|---|
| **HUAN_LUYEN_VIEN — LOP_TAP** | 1-N | Đặt khóa ngoại `MaHLV` ở bảng **LOP_TAP** (bên nhiều/N). |
| **HOI_VIEN — LOP_TAP** | N-N | Tạo bảng trung gian **PHIEU_DANG_KY_CHI_TIET** (hoặc chuẩn hóa thành 2 bảng: **PHIEU_DANG_KY** chứa `MaHoiVien` và **CHI_TIET_DANG_KY** chứa cặp khóa `MaPhieu`, `MaLop`). |

---

### Phần 3 — Xử lý 2 lỗi chuẩn hóa ở mục 4

| Lỗi ở mục 4 | Vi phạm dạng chuẩn nào | Tách thành bảng nào, gồm cột gì |
|---|---|---|
| `TenLop`, `HocPhi` chỉ phụ thuộc `MaLop` | **2NF** (Phụ thuộc hàm một phần vào khóa chính ghép `MaPhieu + MaLop`) | Tách riêng bảng **LOP_TAP** gồm: `MaLop` (PK), `TenLop`, `HocPhi`, `MaHLV` (FK). |
| `SoDienThoai` phụ thuộc `TenHoiVien` | **3NF** (Phụ thuộc bắc cầu qua thuộc tính không khóa `TenHoiVien`) | Tách riêng bảng **HOI_VIEN** gồm: `MaHoiVien` (PK), `TenHoiVien`, `SoDienThoai`. |