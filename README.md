# CS114

## Mô tả bài toán
- Gợi ý khách sạn dựa vào các thông tin mà người dùng nhập vào khi tìm kiếm khách sạn.
- Ngữ cảnh ứng dụng: được sử dụng trong các trang web đặt khách sạn như booking.com cho những người dùng mới khi họ lần đầu sử dụng các trang web này.

### Input
- Người dùng chọn các thông tin về chuyến đi:
  - Loại chuyến đi: 'business trip', 'leisure trip'.
  - Kích thước phòng: 'single', 'double', 'twin', 'large', 'king', 'queen'.
  - Loại phòng: 'standard', 'classic', 'club', 'junior', 'superior', 'deluxe', 'suite', 'luxury'.
  - Thời gian ở lại khách sạn: 1, 2, 3,... ngày.
  - Số người ở: 'solo', 'couple', 'group', 'family'.
- Người dùng nhập vào một đoạn mô tả các đặc điểm mà họ muốn khách sạn có. Ví dụ: I want a hotel with great sight.

### Output
Danh sách 10 khách sạn xếp theo thứ tự giảm dần về độ phù hợp với yêu cầu của khách hàng.
![image](https://github.com/Cancogang69/CS114/assets/90518328/cf744f89-1cbb-421a-b9be-78b80051b9d0)

### Ràng buộc
- Câu mô tả mà người dùng nhập vào được viết hoàn toàn bằng tiếng Anh.
- Câu mô tả mà người dùng nhập vào phải liên quan tới các danh mục sau: Location, Service, Room, Facility and amenity, Meal.

## Mô tả về bộ dữ liệu
### Nguồn
Tên bộ dữ liệu: 515K Hotel Reviews Data in Europe.
Link: https://www.kaggle.com/datasets/jiashenliu/515k-hotel-reviews-data-in-europe/data.
### Số lượng
- Số lượng điểm dữ liệu: 515738.
- Số lượng đặc trưng: 17.
### Tiền xử lí dữ liệu
- Loại bỏ các điểm dữ liệu bị khuyết.
- Loại bỏ các điểm dữ liệu trùng lặp.
- Loại bỏ các đặc trưng không cần thiết.
### Phân chia train - test
- Tỉ lệ train set: 80%.
- Tỉ lệ test set: 20%.

## Xây dựng bộ từ điển
Chúng tôi xem xét năm mục đánh giá sau đây cho các khách sạn: Location, Service, Room, Facility & Amenity, Meal. Những mục đánh giá này có thể được gọi là các danh mục. Để trích xuất sở thích của người đánh giá từ các đánh giá, chúng tôi đặt giả thiết rằng một người quan tâm đến một danh mục nào đó thường có xu hướng đề cập đến các từ có liên quan đến danh mục đó nhiều lần. Chúng tôi phân loại các từ thuộc vào danh mục nào bằng cách trích xuất một số danh từ trong tập dữ liệu và phân loại chúng thủ công vào năm danh mục bằng cách sử dụng trong đó có sự tham gia của ba người gán nhãn độc lập trên 1001 mẫu dữ liệu. Khi tổng hợp, chúng tôi sử dụng phương pháp Fleiss' Kappa để đo lường mức độ đồng nhất giữa những người đánh giá (Inter-annotator Agreement) và đạt kết quả là 0.55. Sau đó tiến hành chọn ra 689 danh từ có thể được sử dụng để ám chỉ đến danh mục nào đó và xuất hiện thường xuyên nhất trong tập dữ liệu, xây dựng nó thành một từ điển.

## Mô tả về đặc trưng
### Feature engineering
- Câu mô tả:
+ Trích xuất các danh từ trong câu mô tả.
+ Phân loại các danh từ này vào 5 danh mục đã nêu ở phần ràng buộc.
+ Tính mức độ quan trọng của từng danh mục dựa vào số lần xuất hiện của những từ thuộc từng danh mục.
- Trích xuất các tag thuộc vào 5 loại tag đã nêu ở phần input.
### Data processing pipeline
![image](https://github.com/Cancogang69/CS114/assets/90518328/6d8b274f-b976-4e21-ba28-e589c3dbc444)

## Các thuật toán máy học được sử dụng
- Support vector regression.
- Random forest regressor.
- XGBRegressor.

## Cài đặt tinh chỉnh tham số
Hyper parameter tuning sử dụng GridSearchCV của thư viện sklearn.

## Đánh giá kết quả
Dựa vào độ đo root mean square error (RMSE) và mean absolute error (MAE).
