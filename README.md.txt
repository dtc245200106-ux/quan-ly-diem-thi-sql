# Bài thực hành: Tạo CSDL Quản Lý Điểm Thi

## 📋 Thông tin
- **Database:** QuanLyDiemThi
- **Số bảng:** 4
- **Công cụ:** MySQL Workbench

## 📊 Cấu trúc các bảng

### 1. Bảng HocSinh
| Trường | Kiểu | Rộng | Ràng buộc |
|--------|------|------|-----------|
| MaHS | VARCHAR | 20 | PRIMARY KEY |
| TenHS | VARCHAR | 50 | |
| NgaySinh | DATETIME | | |
| Lop | VARCHAR | 20 | |
| GT | VARCHAR | 20 | |

### 2. Bảng MonHoc
| Trường | Kiểu | Rộng | Ràng buộc |
|--------|------|------|-----------|
| MaMH | VARCHAR | 50 | PRIMARY KEY |
| TenMH | VARCHAR | 50 | |
| MaGV | VARCHAR | 20 | FOREIGN KEY |

### 3. Bảng BangDiem
| Trường | Kiểu | Rộng | Ràng buộc |
|--------|------|------|-----------|
| MaHS | VARCHAR | 20 | FK, PK |
| MaMH | VARCHAR | 50 | FK, PK |
| DiemThi | INT | | |
| NgayKT | DATETIME | | |

### 4. Bảng GiaoVien
| Trường | Kiểu | Rộng | Ràng buộc |
|--------|------|------|-----------|
| MaGV | VARCHAR | 20 | PRIMARY KEY |
| TenGV | VARCHAR | 50 | |
| SDT | VARCHAR | 10 | |

## 📝 Câu lệnh SQL

```sql
CREATE DATABASE QuanLyDiemThi;
USE QuanLyDiemThi;

CREATE TABLE GiaoVien(
    MaGV VARCHAR(20) PRIMARY KEY,
    TenGV VARCHAR(50),
    SDT VARCHAR(10)
);

CREATE TABLE HocSinh(
    MaHS VARCHAR(20) PRIMARY KEY,
    TenHS VARCHAR(50),
    NgaySinh DATETIME,
    Lop VARCHAR(20),
    GT VARCHAR(20)
);

CREATE TABLE MonHoc(
    MaMH VARCHAR(50) PRIMARY KEY,
    TenMH VARCHAR(50),
    MaGV VARCHAR(20),
    FOREIGN KEY (MaGV) REFERENCES GiaoVien(MaGV)
);

CREATE TABLE BangDiem(
    MaHS VARCHAR(20),
    MaMH VARCHAR(50),
    DiemThi INT,
    NgayKT DATETIME,
    PRIMARY KEY (MaHS, MaMH),
    FOREIGN KEY (MaHS) REFERENCES HocSinh(MaHS),
    FOREIGN KEY (MaMH) REFERENCES MonHoc(MaMH)
);