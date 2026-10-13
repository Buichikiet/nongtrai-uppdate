# 🌱 Nông Trại Vui Vẻ – bản Online v2 (Super VIP)

Game nông trại online đa người chơi, đăng nhập Google/Discord, lưu data lên mây, Discord bot tự setup, **sảnh siêu VIP**, **map hoạt hình đẹp**, **nhân vật LED**, **15 role dễ thương**, **shop quần áo/balo/giày/xe**, **điểm danh mỗi ngày**, **ủng hộ MB Bank QR**.

## 1. Chạy thử nhanh (không cần Google/Discord)

```bash
npm install
cp .env.example .env
# mở .env, đặt:  DEV_LOGIN=1   và   OWNER_EMAILS=dev:tenban
npm start
```

Mở `http://localhost:3000` → ở sảnh bấm **📱 Điện thoại** / **💻 PC** → **🧪 Đăng nhập thử** → nhập tên `tenban` → bạn là **OWNER**.

## 2. Đăng nhập thật (Google hoặc Discord)

### 🔵 Google OAuth
1. https://console.cloud.google.com → **APIs & Services → Credentials → Create credentials → OAuth client ID → Web application**.
2. **Authorized JavaScript origins**: thêm domain game của bạn (vd `https://nongtrai.onrender.com`) và `http://localhost:3000` để test.
3. Copy **Client ID** → dán vào `GOOGLE_CLIENT_ID` trong `.env`.
4. Đặt `OWNER_EMAILS=email-google-cua-ban@gmail.com` → tài khoản này tự có role **OWNER** (👑).
5. Khi chạy thật, đặt `DEV_LOGIN=0`.

### 🎮 Discord OAuth
1. https://discord.com/developers/applications → **New Application → Bot** → copy **Application ID** (`DISCORD_CLIENT_ID`) và **Client Secret** (`DISCORD_CLIENT_SECRET`).
2. **OAuth2 → URL Generator**: tick `identify email` → copy **Redirect URI** mà server in ra khi khởi động, thêm vào Discord (vd `https://yourdomain.com/auth/discord/callback`).
3. Có thể bỏ qua OAuth, người chơi vẫn vào Discord → `/lienket ma` để liên kết.

**Sau khi đăng nhập:** sảnh sẽ hiện **mã thành viên 6 ký tự** + nút **▶ Vào game (nhân vật đã có sẵn)**. Bấm thẳng vào chơi, không cần tạo lại nhân vật.

## 3. Bot Discord + `/setup all` (tự setup toàn bộ)

1. https://discord.com/developers/applications → **New Application → Bot** → **Reset Token** → copy vào `DISCORD_TOKEN`.
2. Trong tab **Bot** bật **Message Content Intent**, **Server Members Intent**.
3. **OAuth2 → URL Generator**: tick `bot` + `applications.commands`, quyền **Administrator** → mời bot vào server.
4. Điền `.env`:
   - `DISCORD_GUILD_ID` = ID server Discord (bật Developer Mode → chuột phải server → Copy ID)
   - `DISCORD_OWNER_IDS` = ID Discord của bạn (được dùng `/role` cấp quyền)
   - `DISCORD_ADMIN_IDS` = ID các admin (cách nhau dấu phẩy)
5. Khởi động lại server, sau đó gõ `/setup all` trong Discord — bot sẽ tự tạo:
   - 5 role quyền: 👑 OWNER, 🛡️ ADMIN, 🔧 MOD, 💎 VIP, 📋 Staff, 🌱 Nông Dân
   - **15 role dễ thương** (Thỏ Con, Đào Ngọt, Sao Mai, Kẹo Bông, Hoa Nhài, Ánh Trăng, Mật Ong, Mây Hồng, Tiên Tí Hon, Mèo Bông, Hướng Dương, Bánh Kem, Lấp Lánh, Dâu Tây, Thiên Thần)
   - Kênh: #thong-bao, #diem-danh, #chat-the-gioi, #huong-dan, #tai-game, #ung-ho (kèm QR MB Bank), #tao-ticket, #bao-cao, #dang-nhap (log), #staff-chat
   - **Panel ticket** hỗ trợ (mở/đóng/nhận đơn)
   - **Panel điểm danh** + bảng copy mã
   - Hướng dẫn + tải game + donate

### Danh sách lệnh slash

| Lệnh | Quyền | Việc |
|---|---|---|
| `/setup all` / `/setup role` / `/setup ticket` | Admin+ | Tự setup server (mọi thứ), tạo role, panel ticket |
| `/lock` `/unlock` `[lydo]` | Mod+ | Khóa/mở kênh chat hiện tại |
| `/baocao ma noidung` | mọi người | Tố cáo → gửi đơn vào kênh #bao-cao cho admin nhận |
| `/diemdanh ma` | mọi người | Điểm danh (copy mã từ sảnh) — nhận xu + giày |
| `/caprole thanhvien role` | Admin+ | Cấp 1 trong 15 role dễ thương cho member |
| `/lienket ma` | mọi người | Liên kết Discord ↔ tài khoản game |
| `/xu ma soluong` | Admin | Cộng/trừ xu (số âm = trừ) |
| `/vatpham ma loai id soluong` | Admin | Tặng hạt giống / nông sản / nội thất / quần áo / giày / balo |
| `/thu ma t role` | Owner | Cấp role quyền: player, viieude noidung [xu]` | Admin | Gửi thư vào hòm thư trong game |
| `/role map, mod, admin, owner |
| `/danhhieu ma title` | Admin+ | Cấp 1 trong 15 danh hiệu dễ thương (hiện trên đầu trong game) |
| `/kick` `/mute ma phut` | Mod+ | Đá / cấm chat (0 = bỏ cấm) |
| `/ban` `/unban` | Admin | Khóa / mở khóa tài khoản |
| `/thongbao noidung` | Admin | Thông báo toàn server game |
| `/thongtin ma` | Mod+ | Xem thông tin người chơi |
| `/online` | mọi người | Xem ai đang online |
| `/top` | mọi người | Bảng xếp hạng cấp độ |
| `/huongdan` | mọi người | Hướng dẫn + link tải |

### Ticket & báo cáo
- Bấm **🎫 Mở ticket** ở kênh #tao-ticket → bot tạo kênh riêng cho bạn + staff.
- Staff bấm **✋ Nhận đơn** trong ticket để nhận xử lý.
- Bấm **🔒 Đóng ticket** khi xong.
- `/baocao` gửi đơn vào kênh #bao-cao (admin kênh) — staff bấm **Nhận đơn tố cáo** để xử lý.

### Đăng nhập & thông báo Discord
- Mỗi lần thành viên đăng nhập game → bot tự thông báo vào **#dang-nhap** (kênh admin): tên, mã, email, role.
- Đăng nhập = auto role **🌱 Nông Dân** (tự động khi join server).

## 4. Role trong game

| Role | Hiển thị | Quyền |
|---|---|---|
| 👑 OWNER | `[OWNER]` đỏ hồng | Tất cả + cấp role |
| 🛡️ ADMIN | `[ADMIN]` đỏ | Cộng xu, tặng đồ, thư, ban/unban, thông báo, cấp danh hiệu dễ thương |
| 🔧 MOD | `[MOD]` xanh lá | Kick, cấm chat, xem thông tin |
| 💎 VIP | `[VIP]` tím | Danh hiệu |
| 15 danh hiệu dễ thương | Hiện trên đầu + chat | Admin cấp qua `/caprole` (Discord) hoặc `/danhhieu ma` (trong game hoặc Discord) |

## 5. Sảnh game (vào game)

- 2 nút lớn: **🎮 Đăng nhập Discord** và **🔵 Đăng nhập Google** (server tự render nút Google nếu có `GOOGLE_CLIENT_ID`).
- Sau đăng nhập: hiện **mã 6 ký tự** + nút **▶ Vào game (nhân vật đã có sẵn)**.
- Mã QR **MB Bank 00180599999998 BUI CHI KIET** hiển thị ngay tại sảnh.
- Lần đầu → tạo nhân vật (chỉnh tay + màu da + tóc + áo + mắt + chọn thiết bị).
- Có nút **📖 Hướng dẫn** + **⬇️ Tải game** (PWA — thêm vào màn hình chính để chơi như app).

## 6. Trong game

- 200 map với 12 chủ đề (Phố Hoạt Hình, Đồng Cỏ, Rừng Thu, Tuyết Trắng, Bãi Biển, Sa Mạc, Anh Đào, Núi Đá, Phép Thuật, Kẹo Ngọt, Vườn Cổ Tích, Đảo Thiên Đường).
- 11 cây trồng từ cà rốt đến đào tiên, 5 hàng hóa, 14 nội thất, 11 loại xe (có 5 xe LED), 11 quần áo (3 loại LED), 5 giày (1 LED), 5 balo (2 LED), 7 thú cưng.
- Bật/tắt LED bằng nút 💡 trên đầu game.
- Nhà 6 cấp từ Lều nhỏ đến Lâu đài.
- Mỗi map có giá bán riêng (+1.5%/map), đi buôn lời xu.

## 7. Đưa lên web (mọi trình duyệt / PWA)

- **Render**: New → Web Service → trỏ vào repo. Build: `npm install`, Start: `npm start`. Thêm biến môi trường như `.env`. Gắn **Disk** vào `/data` và đặt `DATA_DIR=/data`.
- **Docker**: `docker build -t nongtrai . && docker run -p 3000:3000 -v nongtrai-data:/data --env-file .env nongtrai`
- Trên điện thoại: mở game → menu trình duyệt → **Thêm vào màn hình chính** → chơi như app full màn hình (PWA với `manifest.json`).
- Muốn tách giao diện: copy `public/`, sửa `public/config.js` (`server` = địa chỉ server, `googleClientId`).

## 8. Giới hạn

- Dữ liệu game do **máy khách gửi lên** (xu, vật phẩm) — người rành kỹ thuật có thể sửa. Lệnh admin là server kiểm soát.
- Lưu bằng file JSON phù hợp vài trăm người chơi; nhiều hơn nên chuyển SQLite/PostgreSQL.
- Chỉ nên đăng nhập 1 thiết bị cùng lúc.

## 9. Ủng hộ 💖

**MB Bank**: `00180599999998` — **BUI CHI KIET** (Admin Bùi Chí Kiệt)
QR: `https://img.vietqr.io/image/MB-00180599999998-compact2.png?accountName=BUI%20CHI%20KIET&addInfo=UNG%20HO%20NONG%20TRAI`

## 10. Cấu trúc

```
nongtrai-online/
├── server.js         # Server chính: HTTP + WebSocket + Auth
├── discord.js        # Bot Discord: /setup all, ticket, role, điểm danh
├── catalog.js        # Danh mục: 15 danh hiệu dễ thương, vật phẩm, role
├── public/
│   ├── index.html    # Game chính (canvas, sprite, map, NPC, shop, LED, ...)
│   ├── config.js     # Cấu hình client (Google Client ID, server URL)
│   ├── manifest.json # PWA manifest (cài như app)
│   ├── huong-dan.html# Trang hướng dẫn
│   └── tai-game.html # Trang tải game
├── data/             # Lưu database (db.json, admin.log, discord-setup.json)
└── .env.example
```

