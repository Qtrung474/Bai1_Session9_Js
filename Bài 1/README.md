# Phân tích lỗi & Bảng Test Cases

## Phân tích lỗi
- **Dòng lệnh sai logic:** `const basePrice = bookingReservation.priceKey;`
- **Nguyên nhân kỹ thuật:** Khi sử dụng Dot Notation (toán tử dấu chấm `.` ví dụ `obj.prop`), JavaScript sẽ tìm kiếm chính xác một thuộc tính có tên là chuỗi "prop" ở bên trong đối tượng. Trong trường hợp này, `bookingReservation.priceKey` sẽ tìm kiếm thuộc tính có tên chữ là "priceKey" trong đối tượng `bookingReservation`. Vì đối tượng không có thuộc tính nào tên là "priceKey" (chỉ có "roomPrice"), nên kết quả trả về là `undefined`.
- **Hệ quả:** Do `basePrice` bị gán giá trị `undefined`, khi thực hiện phép toán `surcharge = basePrice * 0.3`, kết quả của `surcharge` sẽ bị biến thành `NaN` (Not a Number). Tiếp theo đó, `totalAmount = basePrice + surcharge` (tức là `undefined` cộng với `NaN`) cũng sẽ trả về giá trị `NaN`.
- **Cách khắc phục:** Cần sử dụng Bracket Notation (toán tử dấu ngoặc vuông `[]`) khi muốn truy cập một thuộc tính của đối tượng thông qua giá trị của một biến (truy cập động). Cần sửa `bookingReservation.priceKey` thành `bookingReservation[priceKey]`. Khi sử dụng ngoặc vuông, JavaScript sẽ tính toán giá trị của biến `priceKey` (là chuỗi `"roomPrice"`) rồi mới dùng nó để truy xuất thuộc tính `"roomPrice"` của đối tượng, từ đó lấy được giá trị đúng là `1500000`.

## Bảng Test Cases

| Trường hợp kiểm thử | Dữ liệu đầu vào | Kết quả sai thực tế (khi có lỗi) | Kết quả đúng mong đợi |
| :--- | :--- | :--- | :--- |
| Tính tiền cho khách check-in sớm (trước 12h) | `roomPrice`: 1500000<br>`checkInHour`: 9 | Phụ thu: `NaN`<br>Tổng tiền: `NaN` | Phụ thu: 450000<br>Tổng tiền: 1950000 |
| Tính tiền cho khách check-in chuẩn hoặc trễ (từ 12h trở đi) | `roomPrice`: 1500000<br>`checkInHour`: 14 | Phụ thu: 0<br>Tổng tiền: `NaN` | Phụ thu: 0<br>Tổng tiền: 1500000 |
