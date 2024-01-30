# Đồ án môn Máy học (CS114) 
- Đề tài: Hotel Recommendation
- Thành viên nhóm:
  - Nguyễn Đức Tuệ - 21521644
  - Trần Nhật Anh - 21521841
  
## Mô tả bài toán
<img width="454" alt="image" src="https://github.com/Cancogang69/CS114/assets/100010336/0c90edf3-a21e-45e6-97ac-3d7b1f20cedb">

- Mục tiêu của đồ án là khi người dùng nhập vào một đoạn mô tả các đặc điểm mà họ muốn khách sạn có, hệ thống sẽ đưa ra một danh sách các khách sạn được gợi ý dựa vào các thông tin mà người dùng nhập.
- Ngữ cảnh ứng dụng: được sử dụng trong các trang web đặt phòng khách sạn như booking.com, gợi ý khách sạn cho các khách hàng mới sử dụng trang web dựa trên các đặc điểm cụ thể của các khách sạn. Ví dụ, khi người dùng muốn đặt khách sạn ở các khu du lịch biển và muốn khách sạn phải có view biển, nếu sử dụng bộ lọc thì chỉ thể hiện khách sạn có hay không có view biển, trong khi đó hệ thống gợi ý mà nhóm đề xuất sẽ gợi ý dựa trên các thông tin mà khách hàng đã ở đó để lại, như view biển có đẹp hay không.
-	Bài toán Máy học: bài toán dự đoán điểm mà khách hàng sẽ chấm cho một khách sạn.

### Input của bài toán Máy học
-	Điểm đặc trưng của các mục Location, Service, Room, Facility & Amenity, Meal được trích xuất từ câu mà khách hàng nhập vào.
-	Điểm đặc trưng của các mục Location, Service, Room, Facility & Amenity, Meal của khách sạn được trích xuất từ các bình luận mà các khách hàng đã từng ở trước đó để lại 
-	Điểm trung bình của khách sạn (cột Average_Score trong bộ dữ liệu).

### Output của bài toán Máy học
-	Điểm mà mô hình Máy học dự đoán khách hàng sẽ chấm cho một khách sạn.

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
