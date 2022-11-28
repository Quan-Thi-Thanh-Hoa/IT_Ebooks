# Chương 1: Toàn cảnh học máy: 
Chương này giới thiệu rất nhiều lý thuyết căn bản (và thuật ngữ chuyên ngành) mà hầu hết các nhà khoa học dữ liệu đều phải thuộc lòng. Chương này sẽ mang tính khái quát cao (đây là chương duy nhất không có nhiều đoạn mã) và khá đơn giản. Tuy nhiên, bạn nên nắm rõ ngọn ngành trước khi tiếp tục tìm hiểu phần còn lại của cuốn sách. Giờ thì hãy chuẩn bị một ly cà phê và bắt đầu thôi!

## Học Máy là gì?

Học Máy là một môn khoa học (và cả nghệ thuật) về cách lập trình máy tính để chúng có thể học từ dữ liệu.

Dưới đây là định nghĩa tổng quát hơn:

[Học Máy là] lĩnh vực nghiên cứu nhằm giúp máy tính có khả năng học mà không cần lập trình một cách tường minh.

`— Arthur Samuel, 1959`

Và định nghĩa mang tính kỹ thuật hơn:

Một chương trình máy tính được cho là học từ kinh nghiệm E với tác vụ T và phép đo chất lượng P nào đó, nếu chất lượng của tác vụ T, được đo bởi P, cải thiện theo kinh nghiệm E.

`— Tom Mitchell, 1997`

Bộ lọc thư rác chính là một chương trình Học Máy có khả năng học để phân loại đâu là thư rác từ các mẫu cho trước (thư được đánh dấu là rác bởi người dùng) và các mẫu thư thường (không phải thư rác). Tập hợp các mẫu mà hệ thống dùng để học được gọi là tập huấn luyện. Mỗi mẫu dữ liệu huấn luyện được gọi là mẫu huấn luyện (hay mẫu). Trong ví dụ này, tác vụ T là việc gán nhãn thư rác cho thư điện tử mới, kinh nghiệm E là dữ liệu huấn luyện, và ta cần định nghĩa thêm phép đo chất lượng P. Một lựa chọn khả thi cho P là tỷ lệ phân loại thư đúng, và phép đo chất lượng cụ thể này được gọi là độ chính xác. Phép đo này thường được dùng trong các bài toán phân loại.

Nếu chỉ tải xuống một bản sao của trang Wikipedia, máy tính của bạn sẽ có thêm rất nhiều dữ liệu nhưng nó sẽ không tự nhiên làm việc tốt hơn. Do đó việc tải xuống một bản sao của trang Wikipedia không phải là Học Máy.

### Tại sao lại dùng Học Máy?

Hãy xem xét cách viết một bộ lọc thư rác bằng kỹ thuật lập trình truyền thống

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/Screenshot%202022-11-28%20110850.png)

1. Đầu tiên ta cần kiểm tra xem thư rác thường trông như thế nào. Ta có thể phát hiện một số từ hoặc cụm từ (như “4U,” “credit card,” “free,” và “amazing”) hay xuất hiện trong tiêu đề thư. Ta cũng có thể thấy một vài khuôn mẫu khác ở tên người gửi, nội dung thư và ở các phần khác của thư.

2. Nếu ta viết thuật toán nhận diện cho từng khuôn mẫu trên, chương trình sẽ đánh dấu một thư điện tử là thư rác nếu một vài khuôn mẫu đó được tìm thấy.

3. Tiếp đến, ta kiểm thử chương trình và lặp lại hai bước trên cho đến khi đạt mức chất lượng để triển khai.

Vì đây là một bài toán khó, khả năng cao chương trình này sẽ trở thành một danh sách dài các quy luật phức tạp và khó bảo trì.

Trái lại, một bộ lọc thư rác dựa trên các kỹ thuật Học Máy sẽ tự động học được những từ và cụm từ nào là dấu hiệu của thư rác bằng cách nhận diện các khuôn mẫu có tần suất cao bất thường trong các mẫu thư rác so với các mẫu thư bình thường. Chương trình này ngắn hơn hẳn, dễ bảo trì hơn, và rất có thể sẽ chính xác hơn.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/Screenshot%202022-11-28%20111216.png)

Nếu những kẻ gửi thư rác nhận ra rằng các thư điện tử chứa cụm “4U” bị chặn thì sao? Có thể chúng sẽ bắt đầu thay thế “4U” bằng “For U”. Một bộ lọc thư rác được lập trình theo hướng truyền thống sẽ cần được cập nhật để đánh dấu những thư điện tử chứa cụm “For U”. Nếu những kẻ này vẫn cố gắng lách qua bộ lọc thư rác, ta phải luôn phải cập nhật thêm các quy luật mới.

Trái lại, một bộ lọc thư rác dựa trên các kỹ thuật Học Máy sẽ tự động nhận thấy rằng cụm từ “For U” đã bắt đầu xuất hiện nhiều bất thường trong các bức thư rác được đánh dấu bởi người dùng, và nó sẽ bắt đầu đánh dấu các thư này mà không cần sự can thiệp bên ngoài.

Một lĩnh vực khác mà Học Máy tỏa sáng là những bài toán quá phức tạp để có thể giải quyết theo hướng truyền thống hoặc không có sẵn giải thuật. Hãy lấy nhận diện giọng nói làm ví dụ. Giả sử ta muốn viết một chương trình đơn giản có khả năng phân biệt hai từ “one” và “two”. Dễ thấy rằng từ “two” bắt đầu với một âm cao (“T”), nên ta chỉ cần dùng cao độ âm thanh làm tiêu chí phân loại. Nhưng tất nhiên kỹ thuật này không thể hoạt động tốt với hàng ngàn từ được phát âm bởi hàng triệu người khác nhau trong không gian ồn ào và khi có cả tá ngôn ngữ khác nhau. Giải pháp tốt nhất (ít nhất là tại thời điểm viết quyển sách này) là viết một thuật toán có khả năng tự học khi được cung cấp nhiều bản thu âm mẫu của mỗi từ.

Cuối cùng, Học Máy còn có thể giúp con người học (Hình 1.4). Ta có thể kiểm tra các thuật toán học máy để biết những gì mà chúng đã học được (mặc dù việc này có thể trở nên khó khăn đối với một số thuật toán nhất định). Ví dụ, sau khi một bộ lọc thư rác đã được huấn luyện với đủ mẫu thư rác, ta có thể dễ dàng xem được danh sách các từ và tổ hợp từ được thuật toán cho là những dấu hiệu tốt nhất để nhận biết thư rác. Đôi khi chúng sẽ tiết lộ sự tương quan mà ta không hề hay biết hoặc các xu hướng mới, từ đó giúp ta hiểu rõ bài toán hơn. Việc áp dụng các kỹ thuật học máy để khai phá lượng dữ liệu lớn có thể giúp tìm ra các khuôn mẫu mà ta không thể thấy trực tiếp. Đây được gọi là khai phá dữ liệu (data mining).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.4.%20H%E1%BB%8Dc%20M%C3%A1y%20c%C3%B3%20th%E1%BB%83%20gi%C3%BAp%20con%20ng%C6%B0%E1%BB%9Di%20h%E1%BB%8Dc.png)

Tóm lại, Học Máy rất tốt cho:
• Những bài toán mà các giải pháp hiện có đòi hỏi quá nhiều quy luật hoặc cần tinh chỉnh nhiều: một thuật toán Học Máy thường có thể đơn giản hóa mã nguồn và hoạt động tốt hơn so với hướng truyền thống.
• Những bài toán phức tạp mà các phương pháp truyền thống không hoạt động tốt: giải pháp có thể là những kỹ thuật Học Máy tốt nhất.
• Môi trường thay đổi: một hệ thống Học Máy có thể thích ứng với dữ liệu mới.
• Việc khám phá tri thức từ các bài toán phức tạp và lượng dữ liệu lớn.

## Các Ứng dụng Tiêu biểu

Hãy cùng điểm qua một vài ví dụ cụ thể về các tác vụ Học Máy, cũng như một số kỹ thuật để giải quyết các tác vụ đó:

**Phân tích hình ảnh và tự động phân loại sản phẩm trên dây chuyền sản xuất**

Đây là bài toán phân loại ảnh và thường được giải quyết bằng mạng nơ-ron tích chập (Convolutional Neural Network – CNN; sẽ được đề cập trong Tập 2).

**Phát hiện khối u trong ảnh quét não**

Đây là bài toán phân vùng theo nhóm (semantic segmentation), trong đó mọi điểm ảnh đều được phân loại (vì ta cần xác định vị trí chính xác và hình dạng của khối u). CNN cũng là phương pháp thường được sử dụng trong bài toán này.

**Phân loại tin tức tự động**

Đây là bài toán xử lý ngôn ngữ tự nhiên (Natural Language Processing – NLP), cụ thể hơn là phân loại văn bản, được giải quyết bằng mạng nơ-ron hồi tiếp (Recurrent Neural Network – RNN), CNN, hoặc Transformer (sẽ được đề cập trong Tập 2).

**Đánh dấu bình luận phản cảm trong diễn đàn một cách tự động**

Đây cũng là bài toán phân loại văn bản, sử dụng chung các công cụ NLP đã kể trên.

**Tóm tắt tài liệu tự động**

Đây là một nhánh của NLP được gọi là tóm tắt văn bản (text summarization), và cũng sử dụng các công cụ như trên.

**Tạo một chatbot hoặc trợ lý cá nhân**

Bài toán này liên quan đến nhiều tác vụ trong NLP, bao gồm hiểu ngôn ngữ tự nhiên (Natural Language Understanding – NLU) và hệ thống hỏi-đáp.

**Dự báo doanh thu công ty của năm tiếp theo, dựa trên nhiều chỉ số hiệu suất**

Đây là tác vụ hồi quy (nghĩa là dự đoán giá trị) và có thể được giải quyết bằng bất kỳ mô hình hồi quy nào, như Hồi quy Tuyến tính (Linear Regression) hoặc Hồi quy Đa thức (tham khảo Chương 4), SVM hồi quy (tham khảo Chương 5), Rừng Ngẫu nhiên Hồi quy (tham khảo Chương 7), hoặc mạng nơ-ron nhân tạo (artificial neural network – sẽ được đề cập trong Tập 2). Nếu muốn đưa vào mô hình một chuỗi các chỉ số hiệu suất trong quá khứ, ta có thể sử dụng RNN, CNN, hoặc Transformer (sẽ được đề cập trong Tập 2).


**Tương tác với ứng dụng thông qua giọng nói**

Đây là bài toán nhận diện giọng nói (speech recognition) và đòi hỏi ta phải xử lý các đoạn âm thanh. Vì bản thân các đoạn âm thanh là các chuỗi dài và phức tạp, chúng thường được xử lý bằng RNN, CNN hoặc Transformer (sẽ được đề cập trong Tập 2).

**Phát hiện gian lận thẻ tín dụng**

Đây là bài toán phát hiện bất thường (anomaly detection – tham khảo Chương 9). 

**Phân nhóm khách hàng dựa trên sản phẩm tiêu thụ để thiết kế chiến lược tiếp thị khác nhau cho mỗi phân khúc**

Đây là bài toán phân cụm (clustering – tham khảo Chương 9).

**Biểu diễn một tập dữ liệu phức tạp, nhiều chiều trong biểu đồ một cách rõ ràng và hữu ích**

Đây là bài toán trực quan hóa dữ liệu, thường liên quan tới các kỹ thuật giảm chiều (tham khảo Chương 8).

**Gợi ý sản phẩm mà khách hàng có thể sẽ quan tâm dựa trên những sản phẩm mà họ đã mua trong quá khứ**

Đây là bài toán xây dựng hệ thống đề xuất. Một hướng tiếp cận là đưa các đơn hàng trong quá khứ (và các thông tin khác về khách hàng) vào một mạng nơ-ron nhân tạo (sẽ được đề cập trong Tập 2) để dự đoán sản phẩm có khả năng cao sẽ được mua tiếp theo. Mạng nơ-ron này thường được huấn luyện với chuỗi các sản phẩm đã mua trong quá khứ của mọi khách hàng.

**Xây dựng bot thông minh biết chơi trò chơi**

Bài toán này thường được giải quyết thông qua Học Tăng Cường (Reinforcement Learning hay RL – sẽ được đề cập trong Tập 2), một nhánh của Học Máy với mục tiêu huấn luyện tác nhân (agent – ở đây là bot) để chọn các hành động sao cho phần thưởng được cực đại hóa theo thời gian (ví dụ, con bot có thể được thưởng mỗi khi người chơi bị mất máu), trong một môi trường cho trước (trường hợp này là trong một trò chơi). Chương trình AlphaGo nổi tiếng từng đánh bại nhà vô địch thế giới trong bộ môn cờ vây đã được xây dựng thông qua RL.

Danh sách này còn rất rất dài, nhưng hy vọng những ví dụ trên đã giúp bạn nắm được phần nào về độ rộng và phức tạp của các tác vụ mà Học Máy có thể giải quyết cũng như các kỹ thuật tương ứng mà ta có thể áp dụng.

### Các kiểu Hệ thống Học Máy

Có rất nhiều kiểu hệ thống Học Máy khác nhau, và chúng có thể được phân loại thành các hạng mục rộng theo các tiêu chí sau:
• Chúng có được huấn luyện dưới sự giám sát của con người hay không (học giám sát, học không giám sát, học bán giám sát và học tăng cường)
• Chúng có thể học từ các dòng dữ liệu gia tăng hay không (học trực tuyến so với học theo batch)
• Chúng hoạt động bằng cách chỉ đơn thuần so sánh các điểm dữ liệu mới với các điểm dữ liệu đã biết, hay bằng cách phát hiện các khuôn mẫu trong dữ liệu huấn luyện và xây dựng một mô hình dự đoán, tương tự công việc của các nhà khoa học (học dựa trên mẫu so với học dựa trên mô hình).

Các tiêu chí này không xung khắc lẫn nhau, và có thể được kết hợp một cách tùy ý. Ví dụ, một hệ thống lọc thư rác tân tiến có thể học liên tục bằng cách huấn luyện một mô hình mạng nơ-ron sâu trên các mẫu thư rác và thư thông thường mới. Do đó, đây là một hệ thống học trực tuyến, dựa trên mô hình và có giám sát.

Hãy cùng xem xét từng yếu tố trên kỹ hơn một chút.

### Học có Giám sát/không Giám sát
Các hệ thống học máy có thể được phân loại dựa trên mức độ và kiểu giám sát được thực hiện khi chúng đang ở trong giai đoạn huấn luyện. Có bốn hạng mục chính: học có giám sát, học không giám sát, học bán giám sát và học tăng cường.

### Học Có Giám Sát
Trong học có giám sát (supervised learning), tập huấn luyện mà ta đưa vào thuật toán đã bao gồm cả kết quả mong muốn, và kết quả đó được gọi là nhãn (Hình 1.5).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.5.%20M%E1%BB%99t%20t%E1%BA%ADp%20hu%E1%BA%A5n%20luy%E1%BB%87n%20%C4%91%C3%A3%20%C4%91%C6%B0%E1%BB%A3c%20g%C3%A1n%20nh%C3%A3n%20cho%20t%C3%A1c%20v%E1%BB%A5%20ph%C3%A2n%20lo%E1%BA%A1i%20th%C6%B0%20r%C3%A1c%20.png)

Một tác vụ học có giám sát điển hình là phân loại (classification). Bộ lọc thư rác là ví dụ tiêu biểu cho tác vụ này: nó được huấn luyện với nhiều mẫu thư điện tử cùng với nhãn tương ứng (thư rác hoặc thư thông thường), từ đó học cách phân loại các thư điện tử mới.

Một tác vụ điển hình khác là dự đoán giá trị số mục tiêu, chẳng hạn như giá xe hơi từ một tập hợp các đặc trưng cho trước (số dặm, tuổi xe, hãng xe, v.v) được gọi là yếu tố dự đoán (predictor). Tác vụ này có tên gọi là hồi quy (regression – Hình 1.6).1 Để huấn luyện hệ thống này, ta cần cung cấp cho nó rất nhiều các mẫu xe hơi cùng các yếu tố dự đoán và nhãn của chúng (giá xe).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh1.6.M%E1%BB%99t%20b%C3%A0i%20to%C3%A1n%20h%E1%BB%93i%20quy%20d%E1%BB%B1%20%C4%91o%C3%A1n%20m%E1%BB%99t%20gi%C3%A1%20tr%E1%BB%8B%20d%E1%BB%B1a%20tr%C3%AAn%20%C4%91%E1%BA%B7c%20tr%C6%B0ng%20%C4%91%E1%BA%A7u%20v%C3%A0o.png)

**Ghi chú**
Trong Học Máy, thuộc tính (attribute) là một kiểu dữ liệu (ví dụ: “số dặm”), trong khi đặc trưng (feature) có thể có nhiều nghĩa tùy thuộc vào ngữ cảnh. Nhìn chung, một đặc trưng là một thuộc tính đi kèm với giá trị của nó (ví dụ, “số dặm = 15,000”). Tuy nhiên, nhiều người thường sử dụng hai từ thuộc tính và đặc trưng với ý nghĩa giống nhau.

Lưu ý rằng một số thuật toán hồi quy cũng có thể được sử dụng để phân loại và ngược lại. Ví dụ, Hồi quy Logistic (Logistic Regression) thường được sử dụng để phân loại, bởi nó có thể trả về một giá trị tương ứng với xác suất mà mẫu dữ liệu thuộc về một lớp nhất định (ví dụ: 20% khả năng là thư rác).

Sau đây là một số thuật toán học có giám sát quan trọng nhất (được đề cập trong cuốn sách này):
• k-Điểm Gần nhất
• Hồi quy Tuyến tính
• Hồi quy Logistic
• Máy Vector Hỗ trợ
• Cây Quyết định và Rừng Ngẫu nhiên
• Mạng nơ-ron

### Học Không Giám Sát
Trong học không giám sát (unsupervised learning), như bạn đã có thể đoán được, dữ liệu huấn luyện không được gán nhãn (Hình 1.7). Hệ thống cố gắng tự học mà không cần giáo viên.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.7.%20M%E1%BB%99t%20t%E1%BA%ADp%20d%E1%BB%AF%20li%E1%BB%87u%20kh%C3%B4ng%20c%C3%B3%20nh%C3%A3n%20d%C3%A0nh%20cho%20t%C3%A1c%20v%E1%BB%A5%20h%E1%BB%8Dc%20kh%C3%B4ng%20gi%C3%A1m%20s%C3%A1t.png)

Dưới đây là một số thuật toán học không giám sát (đa số sẽ được đề cập trong các Chương 8 và Chương 9).

• Phân cụm (Clustering)
- K-Điểm trung bình (K-Means)
- DBSCAN ([Phương pháp phân cụm dựa trên mật độ (Density-Based Clustering)](https://phamdinhkhanh.github.io/deepai-book/ch_ml/DBSCAN.html))
- Phân cụm phân cấp (Hierarchical Cluster Analysis – HCA)

• Phát hiện bất thường và tính mới (Anomaly detection and novelty detection)
- SVM một lớp (One-class SVM)
- Rừng cô lập (Isolation Forest)

• Trực quan hóa (visualization) và giảm chiều (dimensionality reduction)
- Phân tích thành phần chính (Principal Component Analysis – PCA)
- PCA hạt nhân (Kernel PCA)
- Embedding tuyến tính cục bộ (Locally Linear Embedding – LLE)
- Embedding lân cận ngẫu nhiên theo phân phối t (t-Distributed Stochastic Neighbor Embedding - t-SNE)

• Học luật kết hợp (Association rule)
- Apriori
- Eclat

Giả sử bạn có rất nhiều dữ liệu về người đọc blog của mình. Bạn có thể sẽ muốn chạy một thuật toán phân cụm để phát hiện các nhóm người đọc giống nhau (Hình 1.8). Bạn không hề cho thuật toán biết mỗi người thuộc nhóm nào mà nó sẽ phải tự tìm các mối liên kết. Ví dụ, thuật toán có thể thấy rằng 40% người đọc là nam giới, thích đọc truyện tranh và thường đọc blog của bạn vào buổi tối, trong khi 20% còn trẻ, thích khoa học viễn tưởng và thường đọc blog vào cuối tuần. Nếu bạn sử dụng thuật toán phân cụm phân cấp, mỗi nhóm có thể được phân chia thành các nhóm nhỏ hơn. Việc phân cụm có thể giúp bạn viết bài nhắm đến từng nhóm.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.8.%20Ph%C3%A2n%20c%E1%BB%A5m.png)

Các thuật toán trực quan hóa cũng là ví dụ tiêu biểu của học không giám sát: ta đưa vào rất nhiều dữ liệu phức tạp, không có nhãn, và thuật toán trả về biểu diễn hai hoặc ba chiều của dữ liệu, có thể được minh họa dễ dàng bằng đồ thị (Hình 1.9). Các thuật toán này cố gắng giữ nguyên cấu trúc nhiều nhất có thể (ví dụ như giữ các cụm phân biệt trong không gian đầu vào không chồng lấn lên nhau khi biểu diễn), nên ta có thể hiểu cách dữ liệu được tổ chức và xác định các khuôn mẫu ẩn trong dữ liệu.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.9.%20V%C3%AD%20d%E1%BB%A5%20tr%E1%BB%B1c%20quan%20h%C3%B3a%20b%E1%BA%B1ng%20t-SNE%20cho%20c%C3%A1c%20c%E1%BB%A5m%20ng%E1%BB%AF%20ngh%C4%A9a.png)

Một tác vụ liên quan là _giảm chiều_, với mục tiêu là đơn giản hóa dữ liệu mà không làm mất quá nhiều thông tin. Một phương pháp khả thi là gộp các đặc trưng tương quan với nhau thành một. Ví dụ, quãng đường đi được của một chiếc xe có thể tương quan mạnh với tuổi thọ của chiếc xe đó, nên thuật toán giảm chiều sẽ gộp chúng lại thành một đặc trưng biểu diễn sự hao mòn của chiếc xe. Đây được gọi là trích xuất đặc trưng (feature extraction).

### Mẹo
Giảm chiều dữ liệu huấn luyện trước khi đưa chúng vào một thuật toán Học Máy (ví dụ như một thuật toán học có giám sát) thường là một ý tưởng tốt. Thuật toán sẽ chạy nhanh hơn, dữ liệu sẽ chiếm ít dung lượng ổ cứng và bộ nhớ hơn, và trong một vài trường hợp có thể đem lại chất lượng tốt hơn.

Một tác vụ không giám sát quan trọng khác là phát hiện bất thường, ví dụ như phát hiện các giao dịch thẻ tín dụng bất thường để ngăn chặn sai phạm, bắt lỗi trong dây chuyền sản xuất, hoặc tự động loại bỏ các điểm ngoại lại trong tập dữ liệu trước khi đưa chúng vào các thuật toán học. Hệ thống được huấn luyện trên hầu hết các mẫu bình thường nên có thể nhận ra các mẫu này. Sau đó, khi thấy một mẫu mới, hệ thống có thể chỉ ra mẫu này là bình thường hay bất thường (tham khảo Hình 1.10). Một tác vụ tương tự là phát hiện tính mới. Tác vụ này nhắm đến việc phát hiện các điểm không giống các điểm khác trong tập huấn luyện. Tác vụ này đòi hỏi một tập huấn luyện rất “sạch”, không hề chứa các điểm mà thuật toán sẽ cần phải phát hiện. Ví dụ, nếu bạn có hàng nghìn ảnh chó, và 1% số ảnh đó là của giống chó Chihuahua, thuật toán phát hiện tính mới sẽ không xét các bức ảnh Chihuahua mới là ảnh có tính mới. Mặt khác, các thuật toán phát hiện bất thường vẫn có thể xem giống chó này là hiếm và khác các giống chó còn lại, nên có lẽ sẽ phân loại chúng là bất thường (ở đây không có ý kì thị Chihuahua).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.10.%20Ph%C3%A1t%20hi%E1%BB%87n%20b%E1%BA%A5t%20th%C6%B0%E1%BB%9Dng.png)

Cuối cùng, một tác vụ không giám sát phổ biến khác là học luật kết hợp (association rule learning), với mục tiêu là đào sâu vào lượng lớn dữ liệu để khám phá các mối quan hệ thú vị giữa các thuộc tính. Để lấy ví dụ, giả sử bạn sở hữu một siêu thị. Việc áp dụng luật kết hợp cho các hóa đơn bán hàng có thể hé lộ rằng người mua sốt BBQ và bim bim có xu hướng mua thêm thịt bò. Nhờ đó, bạn có thể đặt các mặt hàng này gần nhau.

### Học bán giám sát

Sự tốn kém về thời gian lẫn chi phí của quá trình gán nhãn dữ liệu dẫn đến hệ quả là chỉ một phần nhỏ dữ liệu được gán nhãn. Các thuật toán có thể làm việc với tập dữ liệu được gán nhãn một phần được gọi là thuật toán học bán giám sát (semisupervised learning – Hình 1.11).

Hình 1.11. Học bán giám sát với hai lớp (hình tam giác và hình vuông): các mẫu chưa gán nhãn (hình tròn) giúp phân loại một đối tượng mới (hình chữ thập) vào lớp hình tam giác thay vì hình vuông, mặc dù nó gần với các hình vuông đã được gán nhãn hơn.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.11.%20H%E1%BB%8Dc%20b%C3%A1n%20gi%C3%A1m%20s%C3%A1t%20v%E1%BB%9Bi%20hai%20l%E1%BB%9Bp.png)

Các dịch vụ lưu trữ ảnh là một ví dụ tiêu biểu, điển hình như Google Photos. Sau khi tải lên tất cả ảnh gia đình của bạn lên đó, chúng sẽ tự động nhận diện cùng một người A xuất hiện trong các ảnh 1, 5 và 11, còn người B xuất hiện ở ảnh 2, 5 và 7. Đây là phần không giám sát của thuật toán (phân cụm). Giờ hệ thống chỉ cần bạn chỉ ra những người này là ai. Bằng cách thêm một nhãn cho mỗi người, hệ thống có thể gán tên cho tất cả mọi người trong ảnh, giúp việc tìm kiếm ảnh trở nên thuận tiện hơn.

Đa phần các thuật toán học bán giám sát là sự kết hợp giữa các thuật toán học không giám sát và có giám sát. Ví dụ, mạng niềm tin sâu (deep belief network – DBN) dựa trên các thành phần không giám sát có tên là máy Boltzmann giới hạn (restricted Boltzmann machine – RBM) chồng lên nhau. RBM được huấn luyện tuần tự theo cơ chế không giám sát, rồi sau đó toàn bộ hệ thống được tinh chỉnh bằng các kỹ thuật có giám sát.

### Học Tăng cường
Học Tăng cường là phương pháp học có cấu trúc rất khác. Hệ thống học trong RL được gọi là tác nhân (agent). Nó có thể quan sát môi trường xung quanh, chọn và thực hiện các hành động, sau đó nhận về điểm thưởng – reward (hoặc lượng phạt – penalty dưới dạng điểm thưởng âm, như trong Hình 1.12). Hệ thống sau đó cần tự học chiến lược tốt nhất để nhận về nhiều điểm thưởng nhất qua thời gian, và chiến lược này được gọi là chính sách (policy). Một chính sách định nghĩa hành động mà tác nhân nên chọn khi ở trong một tình huống cụ thể.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.12.%20H%E1%BB%8Dc%20T%C4%83ng%20c%C6%B0%E1%BB%9Dng.png)

Ví dụ, nhiều rô bốt được lập trình với thuật toán học tăng cường để học cách đi lại. AlphaGo của DeepMind cũng là một ví dụ về học tăng cường: nó xuất hiện trên trang nhất của các bản tin trong tháng 5 năm 2017 khi đánh bại nhà vô địch cờ vây thế giới Ke Jie (Kha Khiết). AlphaGo đã học được chính sách dẫn đến chiến thắng bằng cách phân tích hàng triệu ván cờ, rồi tự chơi rất nhiều ván với chính nó. Chú ý rằng AlphaGo không học trong khi thi đấu với Ke Jie mà chỉ đơn thuần áp dụng chính sách nó đã học được từ trước.

### Học theo Batch và Học Trực tuyến
Một tiêu chí khác để phân loại các hệ thống Học Máy nằm ở việc chúng có thể liên tục học từ các dòng dữ liệu gia tăng hay không.

### Học theo Batch
Các hệ thống học theo batch không có khả năng học gia tăng: chúng phải được huấn luyện bằng tất cả dữ liệu khả dụng. Nhìn chung thì việc này sẽ tốn rất nhiều thời gian và tài nguyên tính toán, nên quá trình huấn luyện thường diễn ra một cách ngoại tuyến. Đầu tiên, hệ thống được huấn luyện và hoàn tất việc học trước khi được triển khai thực tế. Trong quá trình triển khai thực tế, hệ thống chỉ áp dụng lại những gì đã được học. Đây được gọi là học ngoại tuyến (offline learning). Nếu ta muốn một hệ thống học theo batch cập nhật thêm dữ liệu mới (ví dụ như một loại thư rác mới), ta cần huấn luyện một phiên bản mới của hệ thống từ đầu với toàn bộ dữ liệu (bao gồm cả dữ liệu mới và cũ), rồi thay hệ thống cũ bằng hệ thống mới.

May mắn là toàn bộ quá trình huấn luyện, đánh giá và triển khai một hệ thống Học Máy có thể được tự động hóa một cách khá dễ dàng (minh họa trong Hình 1.3), nên ngay cả một hệ thống học theo batch cũng có thể thích ứng với thay đổi. Ta chỉ cần cập nhật dữ liệu và huấn luyện một phiên bản mới lại từ đầu khi cần thiết.

Phương án này đơn giản và thường hoạt động tốt, nhưng huấn luyện trên toàn bộ dữ liệu có thể tốn hàng giờ, nên hệ thống thường được huấn luyện lại chỉ sau 24 giờ hoặc thậm chí sau mỗi tuần. Nếu hệ thống cần thích ứng với dữ liệu thay đổi nhanh (ví dụ như giá cổ phiếu), ta sẽ cần một giải pháp linh hoạt hơn.

Thêm vào đó, huấn luyện trên toàn bộ dữ liệu tiêu tốn rất nhiều tài nguyên tính toán (CPU, dung lượng bộ nhớ và ổ đĩa, I/O ổ đĩa và mạng, v.v.). Nếu có rất nhiều dữ liệu, việc tự động huấn luyện lại mô hình hàng ngày có thể tiêu tốn rất nhiều tiền. Nếu lượng dữ liệu có kích thước khổng lồ, học theo batch còn có thể trở nên bất khả thi.

Cuối cùng, nếu hệ thống cần có khả năng học độc lập với tài nguyên hạn chế (ví dụ như ứng dụng điện thoại thông minh hoặc rover trên Sao Hoả), việc lưu trữ lượng lớn dữ liệu huấn luyện và sử dụng nhiều tài nguyên để huấn luyện hàng giờ mỗi ngày là không thể.

May mắn thay, chúng ta có một lựa chọn tốt hơn cho tất cả các trường hợp trên, đó là sử dụng các thuật toán có khả năng học gia tăng.

### Học Trực tuyến
Trong học trực tuyến (online learning), ta huấn luyện mô hình một cách gia tăng bằng cách tuần tự truyền dữ liệu theo từng điểm dữ liệu hoặc theo lô nhỏ gọi là mini-batch. Mỗi bước học rất nhanh và không tốn nhiều tài nguyên, nên hệ thống có thể dễ dàng học với dữ liệu mới khi cần (tham khảo Hình 1.13).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.13.%20Trong%20h%E1%BB%8Dc%20tr%E1%BB%B1c%20tuy%E1%BA%BFn%2C%20m%C3%B4%20h%C3%ACnh%20%C4%91%C6%B0%E1%BB%A3c%20hu%E1%BA%A5n%20luy%E1%BB%87n%20v%C3%A0%20tri%E1%BB%83n%20khai%20th%E1%BB%B1c%20t%E1%BA%BF%2C%20r%E1%BB%93i%20ti%E1%BA%BFp%20t%E1%BB%A5c%20h%E1%BB%8Dc%20khi%20c%C3%B3.png)

Hình 1.13. Trong học trực tuyến, mô hình được huấn luyện và triển khai thực tế, rồi tiếp tục học khi có dữ liệu mới.

Học trực tuyến là giải pháp tốt cho các hệ thống nhận dữ liệu là các luồng liên tục (như giá cổ phiếu) và cần thích ứng với thay đổi một cách nhanh chóng hoặc độc lập. Phương pháp này cũng là lựa chọn tốt nếu tài nguyên tính toán bị giới hạn: một khi hệ thống đã học xong từ dữ liệu mới, dữ liệu này không còn cần thiết nữa và có thể được loại bỏ (trừ khi ta muốn quay lại trạng thái trước đó và “nạp lại” dữ liệu). Điều này giúp tiết kiệm rất nhiều dung lượng lưu trữ.

Các thuật toán học trực tuyến cũng có thể được sử dụng để huấn luyện hệ thống trên các tập dữ liệu khổng lồ và không nằm vừa trong bộ nhớ chính (đây được gọi là học ngoài bộ nhớ chính – out-of-core learning). Thuật toán chỉ nạp một phần dữ liệu, huấn luyện trên phần đó, rồi lặp lại quá trình cho tới khi đã chạy trên toàn bộ dữ liệu (tham khảo Hình 1.14).

### Lưu ý
Học ngoài bộ nhớ chính thường được thực hiện ngoại tuyến (không được thực hiện trên hệ thống đang được triển khai), nên cái tên học trực tuyến có thể sẽ gây hiểu lầm. Hãy nghĩ về nó như là học gia tăng.

Một tham số quan trọng trong các hệ thống học trực tuyến là tốc độ thích ứng với dữ liệu đang thay đổi: tham số này được gọi là tốc độ học (learning rate). Nếu tốc độ học cao, hệ thống sẽ nhanh chóng thích ứng với dữ liệu mới, nhưng cũng sẽ có xu hướng quên dữ liệu cũ nhanh hơn (ta không muốn một bộ lọc thư rác chỉ lọc các loại thư rác nó thấy gần đây nhất). Ngược lại, nếu tốc độ học thấp, hệ thống sẽ có sức ỳ lớn hơn – tức sẽ học chậm hơn, nhưng cũng sẽ bớt nhạy cảm với nhiễu trong dữ liệu mới hoặc với chuỗi dữ liệu không có tính đại diện (ngoại lai).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.14.%20S%E1%BB%AD%20d%E1%BB%A5ng%20h%E1%BB%8Dc%20tr%E1%BB%B1c%20tuy%E1%BA%BFn%20cho%20c%C3%A1c%20t%E1%BA%ADp%20d%E1%BB%AF%20li%E1%BB%87u%20kh%E1%BB%95ng%20l%E1%BB%93.png)

_Hình 1.14. Sử dụng học trực tuyến cho các tập dữ liệu khổng lồ_

Một thách thức lớn với học trực tuyến là nếu dữ liệu kém chất lượng được đưa vào mô hình,
chất lượng của mô hình sẽ giảm. Nếu đó là một hệ thống trực tiếp (live system), khách hàng sẽ
nhận ra. Ví dụ, dữ liệu kém chất lượng có thể đến từ một cảm biến bị hỏng trên rô bốt, hoặc
từ một người đang cố gắng đánh lừa công cụ tìm kiếm để kết quả của họ nằm ở vị trí đầu trên
trang tìm kiếm. Để giảm thiểu rủi ro này, ta cần giám sát hệ thống chặt chẽ và ngay lập tức
dừng huấn luyện (và có thể quay lại trạng thái hoạt động tốt trước đó) khi phát hiện thấy chất
lượng của mô hình giảm đi đáng kể. Ta cũng có thể giám sát dữ liệu đầu vào và xử lý dữ liệu
bất thường (ví dụ, bằng cách sử dụng một thuật toán phát hiện bất thường).

### Học dựa trên Mẫu và dựa trên Mô hình
Một cách khác để phân loại các thuật toán học máy là dựa vào cách chúng khái quát hóa. Phần lớn các tác vụ học máy sẽ xoay quanh việc đưa ra dự đoán. Nghĩa là với các mẫu dữ liệu huấn luyện cho trước, mô hình cần có khả năng đưa ra những dự đoán tốt (khái quát hóa tốt) đối với các mẫu dữ liệu mà nó chưa từng thấy. Việc có một phép đo phù hợp để đánh giá quá trình huấn luyện là tốt nhưng vẫn không đủ. Mục tiêu cuối cùng của mô hình là hoạt động tốt trên dữ liệu mới.

Có hai hướng tiếp cận chính để khái quát hóa: học dựa trên mẫu (instance-based learning) và học dựa trên mô hình (model-based learning).

### Học dựa trên Mẫu
Có lẽ phương thức học đơn giản nhất chính là học thuộc lòng. Nếu ta muốn tạo một bộ lọc thư rác theo cách này, nó chỉ cần lọc ra tất cả các thư giống hệt thư được người dùng đánh dấu trước đó là thư rác. Đây không phải là giải pháp tệ nhất, nhưng chắc chắn cũng không phải là giải pháp tốt nhất.

Thay vì chỉ đánh dấu các thư hoàn toàn giống thư rác, bộ lọc cũng có thể được lập trình để phát hiện các thư gần giống với các thư rác đã biết. Để làm vậy, ta cần có một phép đo độ tương đồng (measure of similarity) giữa hai lá thư. Một phép đo độ tương đồng (rất cơ bản) giữa hai lá thư là đếm số từ cùng xuất hiện trong cả hai. Hệ thống sẽ đánh dấu một bức thư là thư rác nếu nó có nhiều từ trùng lặp với một thư rác đã biết.

Phương pháp này được gọi là học dựa trên mẫu (instance-based learning): hệ thống học thuộc các mẫu dữ liệu, rồi khái quát hóa với các mẫu dữ liệu mới bằng việc sử dụng một phép đo độ tương đồng để so sánh với toàn bộ (hoặc một phần) dữ liệu đã học. Ví dụ, trong Hình 1.15, mẫu mới sẽ được gán nhãn là hình tam giác vì đa số các mẫu giống nó nhất đều thuộc lớp hình tam giác.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.15.%20H%E1%BB%8Dc%20d%E1%BB%B1a%20tr%C3%AAn%20m%E1%BA%ABu.png)

_Hình 1.15. Học dựa trên mẫu_

### Học dựa trên Mô hình
Một cách khác để khái quát hóa từ dữ liệu cho trước là xây dựng một mô hình từ dữ liệu rồi dùng mô hình đó để đưa ra các dự đoán. Phương pháp này được gọi là học dựa trên mô hình – model-based learning (Hình 1.16).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.16.%20H%E1%BB%8Dc%20d%E1%BB%B1a%20tr%C3%AAn%20m%C3%B4%20h%C3%ACnh.png)

Ví dụ, giả sử ta muốn biết tiền có làm con người hạnh phúc hay không, nên ta tải xuống tập dữ liệu Better Life Index từ trang web của OECD, và thống kê về tổng sản phẩm quốc nội (GDP) bình quân đầu người từ trang web của IMF. Sau đó ta gộp hai bảng lại và sắp xếp theo GDP đầu người. Bảng 1.1 là một phần được trích từ bảng này. Hãy vẽ đồ thị cho dữ liệu của các nước trên (Hình 1.17 Hình 1.17. Bạn có nhận thấy xu hướng nào không?).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.17.%20B%E1%BA%A1n%20c%C3%B3%20nh%E1%BA%ADn%20th%E1%BA%A5y%20xu%20h%C6%B0%E1%BB%9Bng%20n%C3%A0o%20kh%C3%B4ng.png)

Chúng ta có thể thấy một xu hướng ở đây! Mặc dù dữ liệu có nhiễu (tức là phần nào đó có tính ngẫu nhiên), ta vẫn nhận ra rằng mức độ hài lòng về cuộc sống dường như tăng lên tuyến tính với GDP đầu người. Do đó, ta quyết định mô hình hóa mức độ hài lòng bằng một hàm tuyến tính theo GDP đầu người. Bước này được gọi là lựa chọn mô hình: ta chọn một mô hình tuyến tính của mức độ hài lòng với duy nhất một thuộc tính là GDP đầu người (Phương trình 1.1).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/Ph%C6%B0%C6%A1ng%20tr%C3%ACnh%201.1.%20M%E1%BB%99t%20m%C3%B4%20h%C3%ACnh%20tuy%E1%BA%BFn%20t%C3%ADnh%20%C4%91%C6%A1n%20gi%E1%BA%A3n.png)

Mô hình này có hai tham số (model parameter) là θ0 và θ1. 5 Bằng cách thay đổi tham số này, mô hình có thể biểu diễn bất kỳ hàm tuyến tính nào, như trong Hình 1.18.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.18.%20M%E1%BB%99t%20v%C3%A0i%20h%C3%A0m%20tuy%E1%BA%BFn%20t%C3%ADnh%20kh%E1%BA%A3%20thi.png)

Trước khi có thể sử dụng mô hình, ta cần chọn giá trị cho các tham số θ0 và θ1. Làm sao để biết giá trị nào giúp mô hình hoạt động tốt nhất? Để trả lời câu hỏi này, ta cần chỉ định một phép đo chất lượng. Ta có thể định nghĩa một hàm lợi ích – utility function (hoặc hàm khớp – fitness function) để đo độ tốt của mô hình, hoặc một hàm chi phí (cost function) để đo độ tệ của mô hình đó. Với các bài toán Hồi quy Tuyến tính, ta thường dùng một hàm chi phí để đo khoảng cách giữa dự đoán của mô hình và mẫu huấn luyện, với mục tiêu là cực tiểu hóa khoảng cách này.

Đây là lúc thuật toán Hồi quy Tuyến tính phát huy tác dụng: chỉ cần đưa vào các mẫu huấn luyện và thuật toán sẽ tìm các tham số giúp mô hình tuyến tính khớp dữ liệu tốt nhất. Quá trình này được gọi là huấn luyện mô hình. Trong trường hợp của ta, thuật toán tìm được các giá trị tham số tối ưu là $θ0 = 4.85$ và $θ1 = 4.91×10^{-5}$

```
Lưu ý
Cùng một từ “mô hình” có thể hiểu là kiểu mô hình (như Hồi quy Tuyến tính), kiến trúc mô hình được định nghĩa hoàn toàn (fully-specified model architecture – như Hồi quy Tuyến tính một đầu vào một đầu ra), hoặc mô hình đã được huấn luyện cuối cùng (final trained model) và sẵn sàng đưa ra dự đoán (như Hồi quy Tuyến tính có một đầu vào và một đầu ra, với $θ0 = 4.85$ và $θ1 = 4.91×10^{-5}$). Việc lựa chọn mô hình bao gồm chọn kiểu mô hình và định nghĩa toàn bộ kiến trúc của nó. Huấn luyện mô hình là chạy một thuật toán để tìm tham số mô hình sao cho dữ liệu được khớp tốt nhất (và hy vọng có thể dự đoán tốt trên dữ liệu mới).
```

Giờ mô hình đã khớp tốt nhất có thể với dữ liệu huấn luyện (với một mô hình tuyến tính), như có thể thấy trong Hình 1.19.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.19.%20M%C3%B4%20h%C3%ACnh%20tuy%E1%BA%BFn%20t%C3%ADnh%20kh%E1%BB%9Bp%20d%E1%BB%AF%20li%E1%BB%87u%20hu%E1%BA%A5n%20luy%E1%BB%87n%20t%E1%BB%91t%20nh%E1%BA%A5t.png)

Cuối cùng thì mô hình đã sẵn sàng để đưa ra dự đoán. Ví dụ, giả sử ta muốn biết mức độ hạnh phúc của người Cộng hoà Síp, nhưng dữ liệu OECD lại không có câu trả lời. Rất may mắn, mô hình có thể đưa ra một dự đoán tốt: ta tra cứu GDP đầu người của Cộng hoà Síp và biết con số đó là $22,587$, rồi áp dụng mô hình và tính được mức độ hài lòng về cuộc sống nằm đâu đó quanh mức $4.85 + 22,587×4.91×10^{-5} = 5.96.$

Để giúp mọi thứ trở nên thú vị hơn, Ví dụ 1.1 chứa mã nguồn Python để nạp, chuẩn bị dữ liệu, minh họa trực quan bằng đồ thị phân tán, rồi huấn luyện một mô hình tuyến tính và đưa ra dự đoán.

```
Phần này thay bằng link (https://colab.research.google.com/drive/1C7YVPcfKSOI-g7ebv8RC8FR8mukIDv7X#scrollTo=DX-tAqWpABUQ)
Phần code bên dưới này nên bỏ qua vì bug, đọc code trong colab nhé!
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import sklearn.linear_model
# Load the data
oecd_bli = pd.read_csv("oecd_bli_2015.csv", thousands=',')
gdp_per_capita = pd.read_csv("gdp_per_capita.csv",thousands=',',delimiter='\t',

encoding='latin1', na_values="n/a")

# Prepare the data
country_stats = prepare_country_stats(oecd_bli, gdp_per_capita)
X = np.c_[country_stats["GDP per capita"]]
y = np.c_[country_stats["Life satisfaction"]]
# Visualize the data
country_stats.plot(kind='scatter', x="GDP per capita", y='Life satisfaction')
plt.show()
# Select a linear model
model = sklearn.linear_model.LinearRegression()
# Train the model
model.fit(X, y)
# Make a prediction for Cyprus
X_new = [[22587]] # Cyprus's GDP per capita
print(model.predict(X_new)) # outputs [[ 5.96242338]]
```
### Ghi chú
Nếu thay vào đó ta sử dụng thuật toán học dựa trên mẫu, ta sẽ nhận thấy rằng Slovenia có GDP đầu người gần giống Cộng hoà Síp nhất ($20,732), và vì dữ liệu OECD cho biết người Slovenia có mức độ hài lòng về cuộc sống là 5.7, ta có thể dự đoán rằng mức độ hài lòng của người Cộng hoà Síp là 5.7. Hai nước gần nhất tiếp theo là Bồ Đào Nha và
Tây Ban Nha với mức độ hài lòng lần lượt là 5.1 và 6.5. Nếu lấy trung bình các giá trị trên, ta thu được 5.77, khá gần với dự đoán của thuật toán học dựa trên mô hình. Thuật toán đơn giản này được gọi là Hồi quy k-Điểm Gần nhất – k-Nearest Neighbors regression (trong ví dụ này thì k = 3).

Việc thay thế mô hình Hồi quy Tuyến tính bằng mô hình k-Điểm Gần nhất trong đoạn mã trên rất đơn giản, bạn chỉ cần thay hai dòng sau:

```
import sklearn.linear_model
model = sklearn.linear_model.LinearRegression()

bằng hai dòng dưới đây:

import sklearn.neighbors
model = sklearn.neighbors.KNeighborsRegressor(n_neighbors=3)
```

Nếu không có vấn đề gì, mô hình sẽ đưa ra các dự đoán tốt. Còn nếu không, ta có thể cần thêm nhiều thuộc tính hơn (tỉ lệ có việc làm, sức khoẻ, ô nhiễm không khí, v.v.), thu thập thêm hoặc cải thiện chất lượng dữ liệu huấn luyện, hoặc có thể chọn một mô hình mạnh hơn (như Hồi quy Đa thức).
Tóm lại, ta đã:
- Nghiên cứu dữ liệu.
- Lựa chọn mô hình.
- Huấn luyện mô hình trên tập dữ liệu huấn luyện (tức sử dụng thuật toán học để tìm kiếm các tham số mô hình sao cho hàm chi phí đạt giá trị nhỏ nhất).
- Và cuối cùng, áp dụng mô hình để đưa ra dự đoán trên dữ liệu mới (việc này được gọi là suy luận – inference), với hy vọng rằng mô hình này sẽ khái quát tốt.

Có thể nói đây là quy trình của một dự án Học Máy điển hình. Trong Chương 2 bạn sẽ được trải nghiệm thực tế với một dự án từ đầu tới cuối.
Cho tới giờ, chúng ta đã đề cập đến khá nhiều kiến thức nền tảng: giờ đây bạn đã biết Học Máy thật sự là gì, tại sao nó lại hữu ích, những loại hệ thống Học Máy phổ biến nhất, và quy trình làm việc của một dự án điển hình. Tiếp theo hãy xem xét những vấn đề có thể xảy ra trong quá trình học, gây ảnh hưởng đến độ chính xác của các dự đoán.

## Những Thách thức Chính của Học Máy
Nói ngắn gọn, vì nhiệm vụ chính của ta là chọn và huấn luyện một thuật toán trên một tập dữ liệu, hai vấn đề có thể xảy ra là “thuật toán tệ” và “dữ liệu xấu”. Hãy bắt đầu với các ví dụ của dữ liệu xấu.

Không đủ Dữ liệu Huấn luyện 

Để dạy một đứa trẻ quả táo là gì, ta chỉ cần chỉ vào quả táo và nói “quả táo” (có thể cần lặp lại quy trình này nhiều lần). Bây giờ đứa trẻ có thể nhận ra quả táo với đủ loại màu sắc và hình
dạng. Quả thật xuất sắc.

Học Máy thì vẫn chưa đạt đến trình độ đó. Hầu hết các thuật toán Học Máy cần rất nhiều dữ liệu để có thể hoạt động hiệu quả. Ngay cả với những bài toán đơn giản, ta cũng cần đến hàng nghìn mẫu, và với những bài toán phức tạp như nhận diện ảnh hoặc giọng nói thì có thể lên đến hàng triệu mẫu (trừ khi ta có thể tận dụng một mô hình có sẵn).

### Sự Hiệu quả Khó lý giải của Dữ liệu
Trong một bài báo nổi tiếng được xuất bản vào năm 2001, hai nhà nghiên cứu của Microsoft là Michele Banko và Eric Brill đã chỉ ra rằng các thuật toán Học Máy rất khác nhau, bao gồm cả những thuật toán khá đơn giản, hoạt động tốt gần như ngang nhau trong cùng một bài toán phức tạp là khử nhập nhằng ngôn ngữ tự nhiên (natural language disambiguation) một khi chúng được cung cấp đủ dữ liệu (có thể thấy trong Hình 1.20). 

Theo lời của các tác giả, “những kết quả này cho thấy rằng chúng ta có thể cần xem xét lại sự đánh đổi giữa việc dành thời gian và tiền bạc để phát triển thuật toán và tập trung làm giàu kho ngữ liệu.”

Ý tưởng về việc dữ liệu quan trọng hơn thuật toán trong các bài toán phức tạp đã được phổ biến hơn nữa bởi Peter Norvig và cộng sự trong bài báo với tiêu đề “The Unreasonable Effectiveness of Data”, xuất bản vào năm 2009.10 Tuy nhiên, cần lưu ý rằng các tập dữ liệu vừa và nhỏ vẫn rất phổ biến, và không phải lúc nào cũng có thể kiếm thêm dữ liệu huấn luyện một cách dễ dàng hoặc ít tốn kém. Vậy nên đừng vội bỏ rơi các thuật toán.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.20.%20T%E1%BA%A7m%20quan%20tr%E1%BB%8Dng%20c%E1%BB%A7a%20d%E1%BB%AF%20li%E1%BB%87u%20so%20v%E1%BB%9Bi%20thu%E1%BA%ADt%20to%C3%A1n.png)

### Dữ liệu Huấn luyện Không mang tính Đại diện
Để khái quát hóa tốt, điều quan trọng là dữ liệu huấn luyện phải có tính đại diện cho các trường hợp mới mà ta muốn khái quát hóa. Điều này đúng cho cả phương pháp học dựa trên mẫu hay học dựa trên mô hình.

Ví dụ, tập hợp các quốc gia mà lúc trước ta đã sử dụng để huấn luyện mô hình tuyến tính không có tính đại diện hoàn toàn, vì một vài quốc gia vẫn còn thiếu. Hình 1.21 minh họa dữ liệu sau khi các quốc gia còn thiếu đó được bổ sung.

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.21.%20M%E1%BB%99t%20m%E1%BA%ABu%20hu%E1%BA%A5n%20luy%E1%BB%87n%20c%C3%B3%20t%C3%ADnh%20%C4%91%E1%BA%A1i%20di%E1%BB%87n%20h%C6%A1n.png)

Nếu huấn luyện một mô hình tuyến tính trên tập dữ liệu mới này, ta sẽ thu được đường liền, trong khi mô hình cũ được biểu diễn bởi đường chấm. Có thể thấy rằng việc thêm một vài quốc gia bị thiếu không chỉ thay đổi đáng kể mô hình, mà còn giúp ta nhận ra rằng một mô hình tuyến tính đơn giản như vậy sẽ không bao giờ có thể hoạt động tốt. Có vẻ như các quốc gia rất giàu có không hạnh phúc hơn các quốc gia có thu nhập khá (thực chất họ còn có vẻ kém hạnh phúc hơn), và ngược lại, một số quốc gia nghèo lại có vẻ hạnh phúc hơn nhiều quốc gia giàu có.

Bằng cách huấn luyện trên một tập dữ liệu không có tính đại diện, các dự đoán của mô hình khó có thể chính xác, đặc biệt là đối với các nước rất nghèo và rất giàu.

Điều quan trọng ở đây là sử dụng tập huấn luyện có tính đại diện cho các trường hợp mà ta muốn khái quát hóa. Điều này nói dễ hơn làm: nếu lượng mẫu quá nhỏ, ta sẽ có nhiễu do lấy mẫu (sampling noise – dữ liệu không mang tính đại diện do sự ngẫu nhiên), nhưng kể cả lượng mẫu lớn cũng có thể không có tính đại diện bởi sai sót trong phương pháp lấy mẫu. Hiện tượng thứ hai được gọi là thiên kiến lấy mẫu (sampling bias).

### Các ví dụ về Thiên kiến lấy Mẫu

Có lẽ ví dụ nổi tiếng nhất về thiên kiến lấy mẫu xảy ra trong cuộc bầu cử tổng thống Mỹ năm 1936 giữa Landon và Roosevelt: tờ Literary Digest đã tiến hành một cuộc thăm dò khổng lồ bằng cách gửi thư cho khoảng 10 triệu người. Họ nhận được 2.4 triệu hồi âm và dựa vào đó để dự đoán với độ tin cậy cao rằng Landon sẽ nhận được 57% số phiếu bầu.

Tuy nhiên, Roosevelt đã chiến thắng với 62% phiếu bầu. Lỗ hổng trong phương pháp lấy mẫu của Literary Digest là:
- Đầu tiên, để có được địa chỉ cho việc gửi phiếu thăm dò, tờ Literary Digest đã sử dụng danh bạ điện thoại, danh sách người đăng ký tạp chí, danh sách thành viên câu lạc bộ và những nguồn tương tự. Tất cả những danh sách này đều thiên về tầng lớp giàu có, những người khả năng cao sẽ bầu cho Đảng Cộng Hòa (mà Landon là người đại diện).
- Thứ hai, chỉ có ít hơn 25% số người được hỏi đã trả lời. Điều này lại gây ra thiên kiến lấy mẫu bằng cách loại trừ những người không quan tâm nhiều đến chính trị, những người không thích tờ Literary Digest, cũng như nhiều nhóm quan trọng khác. Đây là một dạng đặc biệt của thiên kiến lấy mẫu, thường được gọi là thiên kiến không phản hồi (nonresponse bias).

Một ví dụ khác: giả sử ta muốn xây dựng một hệ thống nhận diện các video nhạc funk. Một cách để xây dựng tập huấn luyện là tìm kiếm từ khóa “nhạc funk” trên Youtube và sử dụng các video thu được. Tuy nhiên, điều này giả định rằng công cụ tìm kiếm của Youtube trả về một tập hợp các video đại diện cho tất cả các video nhạc funk tồn tại trên nền tảng Youtube. Trên thực tế, kết quả tìm kiếm có thể thiên về những nghệ sĩ nổi tiếng (nếu bạn sống ở Brazil, đa số kết quả nhận được là các video “funk carioca”, và chúng nghe hoàn toàn khác so với James Brown). Mặt khác, ta còn có thể làm gì hơn để thu được một tập huấn luyện lớn?

### Dữ liệu Kém Chất lượng
Tất nhiên, nếu tập huấn luyện của bạn chứa đầy lỗi, điểm ngoại lai và nhiễu (chẳng hạn như do sai số đo lường), hệ thống sẽ gặp nhiều khó khăn trong việc phát hiện các khuôn mẫu ẩn, và ít có khả năng hoạt động tốt. Việc dành thời gian làm sạch dữ liệu huấn luyện thường rất cần thiết. Sự thật là đa số các nhà khoa học dữ liệu dành phần lớn thời gian của họ chỉ để làm việc đó. Những ví dụ sau đây là các trường hợp mà ta cần làm sạch dữ liệu huấn luyện:

- Nếu một số mẫu rõ ràng là ngoại lai, ta có thể đơn thuần loại bỏ chúng hoặc sửa lỗi một cách thủ công.
- Với những mẫu bị thiếu một số đặc trưng (ví dụ: 5% khách hàng của bạn không cung cấp tuổi của họ), ta cần quyết định giữa việc bỏ qua luôn thuộc tính này, bỏ qua những mẫu bị thiếu, điền vào các giá trị còn thiếu (ví dụ, bằng tuổi trung vị), hoặc huấn luyện hai mô hình: một mô hình với đặc trưng đó và một mô hình thì không.





[Toàn cảnh Học Máy](https://drive.google.com/drive/folders/1U2bYaRq8guNpDsIaIx4FAQFLmRBLN06g)
