Kính chào anh/chị thuộc ban tuyển dụng công ty DataGenius,

Em tên là Nguyễn Minh Hoàng Đạt, sinh viên năm 3 ngành Khoa học dữ liệu Trường Đại học Khoa Học Tự Nhiên - ĐHQGHCM.

Hiện tại em đang ứng tuyển vị trí Data Analyst Intern và đang thực hiện bài kiểm tra dự án, em xin trình bày 1 số điểm về bài kiểm tra của em như sau:
- Vì phần lớn em thực hành trên google colab nên các config của visual code để tương tác github em chưa thực hiện được, nên em xem trình bày thời gian thực hiện
	+ 18-19/6: crawl data
	+ 20-21/6: phân tích dataset với 2000 sản phẩm
	+ 21/6: crawl comment data của 1 sản phẩm cụ thể
	+ 22-24/6: tiếp tục xử lý với bộ dataset 2000 sản phẩm và thực hiện bài Text_Classification với comment data
- Do lỗi cá nhân, em chỉ crawl data sản phẩm tiki theo danh mục (Sách kiến thức tổng hợp) được 2000 sản phẩm không thể vượt quá 50 trang.
- Dataset với 2000 sản phẩm em có xử lý và sử dụng vài kỹ thuật Feature Engineer để giải quyết 2 hướng.
	+ Dự đoán số lượng sản phẩm bán được (quantity_sold).
	+ Phân loại mặt hàng có thể bán được nhiều số lượng và xu hướng thành mặt hàng phổ biến.
- Tuy nhiên do cá nhân em chưa làm tốt và dataset khá ít nên cả 2 hướng bài toàn em làm chưa có kết quả tốt.

- Em chuyển sang một bài toán khác (tuy không nằm trong yêu cầu nhưng em mong có thể được xem xét phần nào) 
bài toán phân loại đánh giá sao (1-5 sao) dựa vào nội dung đánh giá và các yếu tố đi kèm của 1 sản phẩm cụ thể (Cây Cam Ngọt Của Tôi).
	+ Crawl tất cả đánh giá sao và nội dung đánh giả sản phẩm.
	+ Tiền xử lý: loại bỏ các thuộc tính không cần thiết (id, name...), chuyển thuộc tính ngày giờ về thuộc tính số, giảm high-cardinality, loại bỏ missing values.
	+ Nội dung đánh giá: vì là ngôn ngữ Việt Nam nên em sử dụng 1 file Stop-word vietnamese trên github sau đó xử lý: emoji, tags, dấu câu, tokenization, ...
	+ Loại bỏ 1 dòng nội dung chữ Trung Quốc và trực quan từ ngữ có xu hướng đánh giá 5 sao (đẹp, cẩn thận, ...) cũng như 1 sao (tệ, gãy, ...).
	+ Trực quan hóa dữ liệu số để xem xét phân phối và đưa ra hướng giải quyết: xử lý outlier, feature transformation.
   * Feature Engineering techniques:
	+ Encoding: sử dụng LabelEncoder cho thuộc tính 'title' có dạng ordinal, get_dummies cho thuộc tính 'is_photo' có dạng nominal.
	+ Feature Selection: loại bỏ 1 số thuộc tính gần như constant values và hệ số tương quan cao (multicollinearity).
	+ Feature Transformation: vì impute outlier không cải thiện performance nên thử nghiệm nhiều phương pháp transform thuộc tính số về dạng phân phối chuẩn, 
					ở đây em dùng yeo-johnson, các cách khác như log, nghịch đảo không tốt và box-cox thì không áp dụng giá trị = 0.
	+ Feature Extraction: để xử lý text em dùng TF-IDF để trích xuất mức độ quan trọng của từ trong văn bản, em có thử nghiệm Bag-Of-Word và tokenize - zero padding 
				tuy giảm chiều dữ liệu tuy nhiên các từ sẽ chuyển thành mật độ nên mức độ quan trọng như nhau, không tốt như TF-IDF.
	+ Vì ban đầu Label đã imbalance nên em có hướng một số cách giải quyết class_weight trong model, Stratifed K-fold tuy nhiên em dùng colab thì bị crash, máy em yếu không đáp ứng được
		nên em dùng SMOTE để oversample class thiểu số để tăng data sao cho tất cả các class có tỉ lệ bằng nhau.
	+ Vì feature có text được sử dụng TF-IDF nên em dùng PCA để giảm chiều dữ liệu và em chọn n_components = 7 để giữ information trên 95% để sử dụng Machine Learning.
    * Model
	+ Em có thử xây dựng mô hình neural network tuy nhiên trình độ bản thân chưa đủ tốt, dùng keras_tuner thì kết quả cũng không được tốt, còn LSTM tốn chi phí thời gian. 
	+ Vì không dùng cross-validation với lý do như trên nên em chỉ holdout với train_test_split.
	+ Nên em chỉ dùng GridSearch để tune các model và kết quả tốt nhất em có được là RandomForest(94% accuracy) và XGB(89%) trên bộ data test.

Đây là các quá trình em xử lý bài Text Classification, nếu như em còn vấn đề gì và chưa làm tốt ở đâu em mong anh/chị phản hồi.

Em xin chân thành cảm ơn!
Đạt

