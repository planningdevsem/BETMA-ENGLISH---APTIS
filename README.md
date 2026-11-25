# BETMA ENGLISH — APTIS Practice & Mock Test

Bộ website tĩnh publish bằng GitHub Pages, nhận kết quả qua Google Apps Script và lưu tập trung vào Google Sheets.

## Bảng Admin cần xem

**Chỉ cần mở sheet `APTIS_RESULTS` để xem kết quả thi thử. Mỗi lượt nộp bài = đúng 1 hàng.**

Các cột theo thứ tự:
1. Mã lượt thi
2. Họ và tên thí sinh
3. Số điện thoại
4. Email
5. Điểm Grammar & Vocabulary (đúng/tổng)
6. Điểm Listening (/50)
7. Điểm Reading (/50)
8. Toàn bộ bài Writing (đầy đủ prompt và câu trả lời từng phần trong cùng một ô)
9. Mã đề
10. Thời gian nộp

Một thí sinh thi lại sẽ có một hàng mới. 100 lượt thi được lưu thành 100 hàng; không ghi đè kết quả cũ. Apps Script dùng `LockService` để tuần tự hóa các thao tác ghi và `Submission_ID` để chống ghi trùng khi gửi lại. Website giữ hàng đợi trên trình duyệt và tự thử gửi lại sau lỗi tạm thời; khi người dùng mở lại website, hàng đợi tiếp tục được gửi.

## Các sheet phụ

Các sheet `STUDENT`, `LEADS`, `PRACTICE_HISTORY`, `MOCK_TEST_RESULT`, `ANSWER_DETAIL`, `WRITING_SPEAKING` vẫn được giữ để lưu dữ liệu chi tiết và phục vụ đối soát. Admin không cần ghép các sheet này để xem bảng kết quả chính.

## Thông tin thí sinh

Trước khi thi, thí sinh cần nhập Candidate ID, họ tên, số điện thoại và email. Email được thu ở trường riêng, không còn suy đoán từ Candidate ID. Các trường thông tin này được gửi kèm kết quả.

## Cấu trúc thư mục

```text
index.html
js/
  bank.js
  config.js
assets/
  audio/
  img/
google-apps-script/
  Code.gs
.nojekyll
.gitignore
```

## Cấu hình Google Sheets / Apps Script

Spreadsheet ID đã cấu hình trong `google-apps-script/Code.gs`:
`1YzppiF3cugO-eIZs98mBz6VD7ILPWQs7EeijWBl77OM`

URL Web App đã cấu hình trong `js/config.js`.

Nếu cập nhật Apps Script:
1. Mở Apps Script project hiện tại.
2. Thay toàn bộ nội dung `Code.gs` bằng file `google-apps-script/Code.gs` trong bộ ZIP mới.
3. Save.
4. Chạy `setupSheets()` một lần để tạo sheet `APTIS_RESULTS` và đưa sheet này lên đầu. Cấp quyền nếu được hỏi.
5. Vào **Deploy → Manage deployments → Edit**.
6. Chọn **New version** rồi Deploy để cập nhật Web App hiện tại. Giữ nguyên URL `/exec`.
7. Kiểm tra Google Sheets đã có tab `APTIS_RESULTS`.

## Publish GitHub Pages

1. Tạo repository GitHub.
2. Upload toàn bộ nội dung bên trong thư mục `betma-english` (không upload thư mục cha lồng thêm một cấp).
3. Đảm bảo `index.html` nằm ngay ở root repository.
4. Vào **Settings → Pages**.
5. Chọn **Deploy from a branch**, Branch `main`, Folder `/ (root)`, Save.

## Kiểm thử bắt buộc

1. Dùng một thí sinh test với đủ họ tên, số điện thoại, email.
2. Nộp một đề thi thử.
3. Mở `APTIS_RESULTS`: phải xuất hiện đúng một hàng gồm thông tin, điểm G&V, Listening, Reading và toàn bộ Writing.
4. Nộp thêm một lượt khác: phải xuất hiện hàng mới.
5. Dùng thiết bị/trình duyệt khác nộp một bài: dữ liệu vẫn vào cùng sheet.
6. Thử nhiều lượt nộp gần nhau; mỗi `Submission_ID` chỉ có một hàng.

## Lưu ý về điểm và Writing

- G&V lưu theo định dạng số câu đúng / tổng số câu, đúng với cách giao diện hiện tại hiển thị điểm phần này.
- Listening và Reading lưu theo thang /50 như cách tính hiện tại trong source.
- Writing được lưu đầy đủ theo từng task: tên phần, đề bài và câu trả lời. Nội dung tất cả phần Writing nằm trong cùng một ô của hàng kết quả.
- Speaking không được đưa vào cột Writing. File ghi âm hiện vẫn chỉ lưu metadata ở trình duyệt; muốn thu file âm thanh tập trung cần bổ sung upload lên Google Drive/backend riêng.

## Bảo mật

Web App hiện cho phép nhận dữ liệu công khai để GitHub Pages gửi bài. Đây là cơ chế nhận diện thông tin, không phải xác thực danh tính. Không thu mật khẩu hoặc dữ liệu nhạy cảm. Chỉ chia sẻ Spreadsheet cho nhân sự được phép. Kiểm thử trước khi phát hành rộng rãi.

## Tài liệu

Trước khi đặt repository ở chế độ public, xác nhận quyền phát hành đối với tài liệu bên thứ ba, đặc biệt nội dung Aptis General Practice Tests có thể thuộc bản quyền British Council.
