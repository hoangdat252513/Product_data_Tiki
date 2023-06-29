Phân loại đánh giá sao (1-5 sao) dựa vào nội dung đánh giá và các yếu tố đi kèm của 1 sản phẩm cụ thể (Cây Cam Ngọt Của Tôi).
	+ Crawl tất cả đánh giá sao và nội dung đánh giả sản phẩm với API mở Tiki.
	+ Tiền xử lý: loại bỏ các thuộc tính không cần thiết (id, name...), chuyển thuộc tính ngày giờ về thuộc tính số, giảm high-cardinality, loại bỏ missing values.
	+ Nội dung đánh giá: vì là ngôn ngữ Việt Nam nên sử dụng 1 file Stop-word vietnamese trên github sau đó xử lý: emoji, tags, dấu câu, tokenization, ...
	+ Loại bỏ 1 dòng nội dung chữ Trung Quốc và trực quan từ ngữ có xu hướng đánh giá 5 sao (đẹp, cẩn thận, ...) cũng như 1 sao (tệ, gãy, ...).
	+ Trực quan hóa dữ liệu số để xem xét phân phối và đưa ra hướng giải quyết: xử lý outlier, feature transformation.
   * Feature Engineering techniques:
	+ Encoding: sử dụng LabelEncoder cho thuộc tính 'title' có dạng ordinal, get_dummies cho thuộc tính 'is_photo' có dạng nominal.
	+ Feature Selection: loại bỏ 1 số thuộc tính gần như constant values và hệ số tương quan cao (multicollinearity).
	+ Feature Transformation: vì impute outlier không cải thiện performance nên thử nghiệm nhiều phương pháp transform thuộc tính số về dạng phân phối chuẩn, ở đây dùng yeo-johnson, các cách khác như log, nghịch đảo không tốt và box-cox thì không áp dụng giá trị = 0.
	+ Feature Extraction: để xử lý text em dùng TF-IDF để trích xuất mức độ quan trọng của từ trong văn bản, đã có thử nghiệm Bag-Of-Word và tokenize - zero padding tuy giảm chiều dữ liệu tuy nhiên các từ sẽ chuyển thành mật độ nên mức độ quan trọng như nhau, không tốt như TF-IDF.
	+ Vì ban đầu Label đã imbalance nên một số cách giải quyết class_weight trong model, Stratifed K-fold tuy nhiên em dùng colab thì bị crash, máy em yếu không đáp ứng được nên em dùng SMOTE để oversample class thiểu số để tăng data sao cho tất cả các class có tỉ lệ bằng nhau.
	+ Vì feature có text được sử dụng TF-IDF nên em dùng PCA để giảm chiều dữ liệu và em chọn n_components = 7 để giữ information trên 95% để sử dụng Machine Learning.
    * Model
	+ Vì không dùng cross-validation với lý do như trên nên em chỉ holdout với train_test_split.
	+ Nên em chỉ dùng GridSearch để tune các model và kết quả tốt nhất em có được là RandomForest(94% accuracy) và XGB(89%) trên bộ data test.

![image](https://github.com/hoangdat252513/Product_data_Tiki/assets/83870939/1ed911cf-1568-4675-b101-ba01c80d52b7)
