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

#### Học có Giám sát/không Giám sát
Các hệ thống học máy có thể được phân loại dựa trên mức độ và kiểu giám sát được thực hiện khi chúng đang ở trong giai đoạn huấn luyện. Có bốn hạng mục chính: học có giám sát, học không giám sát, học bán giám sát và học tăng cường.

### Học Có Giám Sát
Trong học có giám sát (supervised learning), tập huấn luyện mà ta đưa vào thuật toán đã bao gồm cả kết quả mong muốn, và kết quả đó được gọi là nhãn (Hình 1.5).

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/Funix/data/H%C3%ACnh%201.5.%20M%E1%BB%99t%20t%E1%BA%ADp%20hu%E1%BA%A5n%20luy%E1%BB%87n%20%C4%91%C3%A3%20%C4%91%C6%B0%E1%BB%A3c%20g%C3%A1n%20nh%C3%A3n%20cho%20t%C3%A1c%20v%E1%BB%A5%20ph%C3%A2n%20lo%E1%BA%A1i%20th%C6%B0%20r%C3%A1c%20.png)









