# tubemix-locales

Bản dịch của [TubeMix Mobile](https://github.com/hien-dev/TubeMix-Mobile), tách khỏi
app để **sửa chữ mà không phải build lại và nộp App Store duyệt**.

```
locales/vi.json  en.json  ko.json  ja.json  zh.json  fr.json
```

App tải file của ngôn ngữ đang dùng rồi đè lên bản đóng sẵn trong bundle:

```
https://raw.githubusercontent.com/hien-dev/tubemix-locales/main/locales/<mã>.json
```

## Sửa thế nào

Sửa thẳng file JSON. Cấu trúc khoá theo đúng `src/i18n/vi.ts` bên repo app.

**Chỗ có biến** dùng `{0}`, `{1}` thay cho `${title}`:

```json
"saveAria": "Thêm {0} vào Yêu thích"
```

**Chỗ chia số ít / số nhiều** dùng cặp `one` / `other`:

```json
"trackCount": { "one": "1 song", "other": "{0} songs" }
```

`one` dùng khi tham số đầu bằng 1. Tiếng Việt, Hàn, Nhật, Trung không chia số nên
chỉ cần một chuỗi. Đủ cho ngôn ngữ hai dạng — **chưa đủ** cho Nga, Ba Lan (4 dạng)
hay Ả Rập (6 dạng).

## Kiểm TRƯỚC khi đẩy

Không có vòng duyệt nào phía sau repo này. Đẩy nhầm là tới thẳng người dùng.

```bash
node ../TubeMix-Mobile/scripts/check-i18n.mjs locales
```

Bật chặn tự động một lần cho mỗi bản sao:

```bash
git config core.hooksPath .githooks
```

## Khi hỏng thì sao

App không bao giờ chết vì repo này. Tải không được, JSON sai, thiếu `{0}` — trường
hợp xấu nhất là người dùng thấy **chữ cũ trong bundle**. Từng khoá hỏng bị bỏ riêng,
những khoá còn lại vẫn áp dụng.

Người dùng nhận bản sửa sau ~5 phút (cache của raw.githubusercontent), kể từ lần
tiếp theo họ mở lại app hoặc đưa app về tiền cảnh.

## Sinh lại từ app

Các file ở đây được xuất ra từ `src/i18n/*.ts`:

```bash
node ../TubeMix-Mobile/scripts/export-locales.mjs
```

Script kiểm khứ hồi — dựng lại từ JSON rồi so từng khoá với hàm gốc — nên bản xuất
không thể lệch nghĩa.

**Sửa ở đây là bản vá nóng.** Nhớ chép lại vào `src/i18n/*.ts` bên app, không thì
bản build sau sẽ quay về chữ cũ cho tới khi app tải lại được file này.
