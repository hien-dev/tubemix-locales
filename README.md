# tubemix-locales

Bản vá chữ hiển thị cho [TubeMix Mobile](https://github.com/hien-dev/TubeMix-Mobile).

App tải `overlay.json` từ repo này rồi **đè lên** bản dịch đóng sẵn trong bundle.
Sửa một chữ dịch sai không cần build lại app, không cần nộp App Store duyệt.

```
https://raw.githubusercontent.com/hien-dev/tubemix-locales/main/overlay.json
```

## Cách sửa

```json
{
  "vi": { "search": { "noResults": "Không tìm thấy kết quả nào." } },
  "ko": { "detail": { "saveAria": "{0}을(를) 즐겨찾기에 추가" } }
}
```

- Mã ngôn ngữ: `vi` `en` `ko` `ja` `zh` `fr`
- Đường dẫn khoá theo đúng cấu trúc `src/i18n/vi.ts` trong repo app
- Khoá dạng hàm dùng `{0}`, `{1}` thay cho `${title}` — **thiếu là app bỏ qua cả khoá đó**
- Khoá không có trong app thì bị bỏ qua, không gây lỗi

## Kiểm TRƯỚC khi đẩy

Không có vòng duyệt nào phía sau repo này. Đẩy nhầm là tới thẳng người dùng.

```bash
cd ../TubeMix-Mobile
node scripts/check-i18n.mjs ../tubemix-locales/overlay.json
```

Có mục nào bị từ chối là exit 1. Sửa cho hết rồi mới commit.

## Khi hỏng thì sao

App không bao giờ chết vì file này. Overlay tải không được, sai định dạng, hay
thiếu biến — trường hợp xấu nhất là người dùng thấy **chữ cũ trong bundle**.

Người dùng nhận bản sửa sau khoảng 5 phút (cache của raw.githubusercontent), kể từ
lần tiếp theo họ mở lại app.
