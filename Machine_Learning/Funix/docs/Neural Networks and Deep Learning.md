# Neural Networks and Deep Learning

Đây là khóa học đầu tiên về chuyên môn học sâu tại [Coursera](https://www.coursera.org/specializations/deep-learning) được kiểm duyệt bởi [DeepLearning.ai](http://deeplearning.ai/) . Khóa học được giảng dạy bởi Andrew Ng.

## Mục lục

* Nói chứ mình lười làm mục lục ý, xin lỗi mn nếu có ai đó đọc nhé!. Và lưu ý chỗ bias nếu đọc đoạn đó nhé. Mong bài đọc sẽ hữu ích cho bạn...

## Tóm tắt Khóa học

Dưới đây là tóm tắt khóa học như được đưa ra trong khóa học [link](https://www.coursera.org/learn/neural-networks-deep-learning):

> Nếu bạn muốn thâm nhập vào AI tiên tiến, khóa học này sẽ giúp bạn làm điều đó. Các kỹ sư học sâu được săn đón rất nhiều và việc thành thạo học sâu sẽ mang đến cho bạn nhiều cơ hội nghề nghiệp mới. Học sâu cũng là một "siêu năng lực" mới cho phép bạn xây dựng các hệ thống AI mà cách đây vài năm không thể thực hiện được.
>
> Trong khóa học này, bạn sẽ tìm hiểu nền tảng của deep learning. Khi bạn kết thúc lớp học này, bạn sẽ:
> - Hiểu các xu hướng công nghệ chính thúc đẩy Deep Learning
> - Có khả năng xây dựng, đào tạo và ứng dụng mạng lưới thần kinh sâu được kết nối đầy đủ
> - Biết cách triển khai mạng nơ ron (vector hóa) hiệu quả
> - Hiểu các tham số chính trong kiến trúc mạng nơ-ron
>
> Khóa học này cũng dạy cho bạn cách Deep Learning thực sự hoạt động, thay vì chỉ trình bày một mô tả lướt qua hoặc ở cấp độ bề mặt. Vì vậy, sau khi hoàn thành nó, bạn sẽ có thể áp dụng học sâu vào ứng dụng của riêng mình. Nếu bạn đang tìm kiếm một công việc trong lĩnh vực AI, sau khóa học này, bạn cũng sẽ có thể trả lời các câu hỏi phỏng vấn cơ bản.

## Giới thiệu về học sâu

> Có thể giải thích các xu hướng chính thúc đẩy sự phát triển của deep learning, đồng thời hiểu nó được áp dụng ở đâu và như thế nào ngày nay.

### NN (Mạng nơ-ron) là gì?

- Nơ-ron đơn == hồi quy tuyến tính mà không áp dụng kích hoạt (perceptron)
- Về cơ bản, một nơ-ron đơn lẻ sẽ tính toán tổng đầu vào có trọng số (W.T*X) và sau đó chúng ta có thể đặt ngưỡng để dự đoán đầu ra trong một perceptron. Nếu tổng đầu vào có trọng số vượt qua ngưỡng, perceptron sẽ kích hoạt và nếu không thì perceptron không dự đoán.
- Perceptron có thể lấy giá trị thực đầu vào hoặc giá trị boolean.
- Trên thực tế, khi w⋅x+b=0 perceptron xuất ra 0.
- Nhược điểm của perceptron là nó chỉ xuất ra các giá trị nhị phân và nếu chúng ta cố gắng cho trọng số và bais thay đổi nhỏ thì perceptron có thể đảo ngược đầu ra. Chúng tôi cần một số hệ thống có thể sửa đổi đầu ra một chút theo thay đổi nhỏ về trọng lượng và độ lệch. Ở đây có chức năng sigmoid trong hình.
- Nếu chúng ta thay đổi perceptron bằng một hàm sigmoid, thì chúng ta có thể thay đổi một chút về đầu ra.
- ví dụ. đầu ra trong perceptron = 0, bạn đã thay đổi một chút trọng số và độ lệch, đầu ra trở thành = 1 nhưng đầu ra thực tế là 0,7. Trong trường hợp sigmoid, output1 = 0, thay đổi nhỏ về trọng số và độ lệch, đầu ra = 0,7.
- Nếu chúng ta áp dụng chức năng kích hoạt sigmoid thì Single nơ ron sẽ đóng vai trò là Hồi quy logistic.
- chúng ta có thể hiểu sự khác biệt giữa hàm perceptron và sigmoid bằng cách nhìn vào biểu đồ hàm sigmoid.

- Đồ thị NN đơn giản:
   - ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/Others/01.jpg)
   - Hình ảnh lấy từ [tutorialspoint.com](http://www.tutorialspoint.com/)
- RELU là viết tắt của rectified linear unit là chức năng kích hoạt phổ biến nhất hiện nay giúp đào tạo NN sâu nhanh hơn.
- Các lớp ẩn tự động dự đoán kết nối giữa các đầu vào, đó là điểm mạnh của deep learning.
- Deep NN bao gồm nhiều lớp ẩn hơn (Deeper layer)
   - ![]([](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/Others/02.png)
   - Hình ảnh lấy từ [opennn.net](http://www.opennn.net/)
- Mỗi Đầu vào sẽ được kết nối với lớp ẩn và NN sẽ quyết định các kết nối.
- Học có giám sát có nghĩa là chúng ta có (X,Y) và chúng ta cần lấy hàm ánh xạ từ X đến Y.

### Học có giám sát với mạng nơ-ron

- Các loại mạng thần kinh khác nhau để học có giám sát bao gồm:
   - CNN hoặc mạng thần kinh tích chập (Hữu ích trong thị giác máy tính)
   - RNN hoặc Mạng thần kinh tái phát (Hữu ích trong Nhận dạng giọng nói hoặc NLP)
   - NN tiêu chuẩn (Hữu ích cho Dữ liệu có cấu trúc)
   - NN hỗn hợp/tùy chỉnh hoặc Bộ sưu tập các loại NN
- Dữ liệu có cấu trúc giống như cơ sở dữ liệu và bảng.
- Dữ liệu phi cấu trúc như hình ảnh, video, âm thanh và văn bản.
- Dữ liệu có cấu trúc mang lại nhiều tiền hơn vì các công ty dựa vào dự đoán về dữ liệu lớn của nó.

### Tại sao học sâu đang phát triển?

### Tại sao học sâu đang phát triển?

- Học sâu đang phát triển vì 3 lý do:
   1. Dữ liệu:
      - Qua hình này ta có thể kết luận:
        - ![]((https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/11.png)
      - Đối với dữ liệu nhỏ NN có thể thực hiện dưới dạng Hồi quy tuyến tính hoặc SVM (Máy vector hỗ trợ)
      - Đối với dữ liệu lớn, NN nhỏ sẽ tốt hơn SVM
      - Đối với dữ liệu lớn, NN lớn tốt hơn NN trung bình tốt hơn NN nhỏ.
      - Hy vọng chúng ta có nhiều dữ liệu vì thế giới đang sử dụng máy tính nhiều hơn một chút
        - Điện thoại di động
        - IOT (Internet vạn vật)
   2. Tính toán:
      - GPU.
      - CPU mạnh mẽ.
      - Phân phối máy tính.
      - ASIC
   3. Thuật toán:
      1. Các thuật toán sáng tạo đã xuất hiện làm thay đổi cách thức hoạt động của NN.
         - Ví dụ: sử dụng hàm RELU tốt hơn nhiều so với sử dụng hàm SIGMOID trong đào tạo NN vì nó giúp giải quyết vấn đề độ dốc biến mất.

## Khái niệm cơ bản về mạng thần kinh

> Học cách thiết lập một bài toán máy học với tư duy mạng thần kinh. Tìm hiểu cách sử dụng vector hóa để tăng tốc các mô hình của bạn.

### Phân loại nhị phân

- Chủ yếu mình muốn nói về cách thực hiện hồi quy logistic để tạo phân loại nhị phân.
   - ![log](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/Others/03.png)
   - Hình lấy từ [3.bp.blogspot.com](http://3.bp.blogspot.com)
- Anh ấy nói về một ví dụ để biết hình ảnh hiện tại có chứa con mèo hay không.
- Dưới đây là một số ký hiệu:
   - `M là số vectơ huấn luyện`
   - `Nx là kích thước của vectơ đầu vào`
   - `Ny là kích thước của vectơ đầu ra`
   - `X(1) là vector đầu vào đầu tiên`
   - `Y(1) là vectơ đầu ra`
   - `X = [x(1) x(2).. x(M)]`
   - `Y = (y(1) y(2).. y(M))`
- Mình sẽ sử dụng python trong khóa học này.
- Trong NumPy, mình có thể tạo ma trận và thực hiện các thao tác trên chúng trong thời gian nhanh chóng và đáng tin cậy.

### Hồi quy logistic

- Thuật toán được sử dụng cho thuật toán phân lớp của 2 lớp.
- Phương trình:
  - Phương trình đơn giản: `y = wx + b`
  - Nếu x là một vectơ: `y = w(transpose)x + b`
  - Nếu chúng ta cần y nằm trong khoảng từ 0 đến 1 (xác suất): `y = sigmoid(w(transpose)x + b)`
  - Trong một số ký hiệu, điều này có thể được sử dụng: `y = sigmoid(w(transpose)x)`
    - Trong khi `b` là `w0` của `w` và chúng ta thêm `x0 = 1`. nhưng mình sẽ không sử dụng ký hiệu này trong khóa học (Andrew nói rằng ký hiệu đầu tiên tốt hơn).
- Trong phân loại nhị phân `Y` phải nằm trong khoảng từ `0` đến `1`.
- Trong phương trình cuối cùng `w` là một vectơ của `Nx` và `b` là một số thực

### Hàm chi phí hồi quy logistic

- Hàm mất mát đầu tiên sẽ là lỗi căn bậc hai: `L(y',y) = 1/2 (y' - y)^2`
  - Nhưng ta sẽ không dùng kí hiệu này vì nó dẫn ta đến bài toán tối ưu không lồi, nghĩa là nó chứa các điểm tối ưu cục bộ.
- Đây là hàm mà chúng ta sẽ sử dụng: `L(y',y) = - (y*log(y') + (1-y)*log(1-y'))`
- Để giải thích chức năng cuối cùng, hãy xem:
  - nếu `y = 1` ==> `L(y',1) = -log(y')` ==> ta muốn `y'` là giá trị lớn nhất ==> `y`' giá trị lớn nhất là 1
  - nếu `y = 0` ==> `L(y',0) = -log(1-y')` ==> chúng ta muốn `1-y'` là lớn nhất ==> `y'` càng nhỏ càng tốt vì nó chỉ có thể có 1 giá trị.
- Khi đó hàm Cost sẽ là: `J(w,b) = (1/m) * Sum(L(y'[i],y[i]))`
- Hàm mất mát tính toán lỗi cho một ví dụ đào tạo duy nhất; hàm chi phí là giá trị trung bình của các hàm mất mát của toàn bộ tập huấn luyện.

### Gradient Descent

- Chúng ta muốn dự đoán `w` và `b` để giảm thiểu hàm chi phí.
- Hàm chi phí của chúng ta là hàm lồi.
- Đầu tiên chúng ta khởi tạo `w` và `b` thành 0,0 hoặc khởi tạo chúng thành một giá trị ngẫu nhiên trong hàm lồi và sau đó cố gắng cải thiện các giá trị để đạt giá trị nhỏ nhất.
- Trong hồi quy Logistic người ta luôn sử dụng 0,0 thay vì ngẫu nhiên.
- Thuật toán gradient khá lặp: `w = w - alpha * dw`
   trong đó alpha là tỷ lệ học tập và `dw` là đạo hàm của `w` (Đổi thành `w`)
   Đạo hàm cũng là hệ số góc của `w`
- Có vẻ như thuật toán tham lam. đạo hàm cung cấp cho chúng ta hướng để cải thiện các tham số của chúng ta.

- Các phương trình thực tế ta sẽ thực hiện:
   - `w = w - alpha * d(J(w,b) / dw)` (hàm dốc bao nhiêu theo hướng w)
   - `b = b - alpha * d(J(w,b) / db)` (hàm dốc bao nhiêu theo hướng d)

### Derivatives

- Chúng ta sẽ nói về một số phép tính cần thiết.
- Bạn không cần phải là một người đam mê giải tích để thành thạo deep learning nhưng bạn sẽ cần một số kỹ năng từ nó.
- Đạo hàm của một đường thẳng là hệ số góc của nó.
   - Ví dụ. `f(a) = 3a` `d(f(a))/d(a) = 3`
   - nếu `a = 2` thì `f(a) = 6`
   - nếu chúng ta di chuyển một chút `a = 2,001` thì `f(a) = 6,003` có nghĩa là chúng ta đã nhân đạo hàm (Độ dốc) với diện tích đã di chuyển và cộng nó vào kết quả cuối cùng.

### Các ví dụ khác về Derivatives

- `f(a) = a^2` ==> `d(f(a))/d(a) = 2a`
   - `a = 2` ==> `f(a) = 4`
   - `a = 2,0001` ==> `f(a) = 4,0004` xấp xỉ.
- `f(a) = a^3` ==> `d(f(a))/d(a) = 3a^2`
- `f(a) = log(a)` ==> `d(f(a))/d(a) = 1/a`
- Tóm lại, Đạo hàm là hệ số góc và hệ số góc khác nhau ở những điểm khác nhau trong hàm, đó là lý do tại sao đạo hàm là một hàm.

### Biểu đồ tính toán

- Là đồ thị tổ chức phép tính từ trái sang phải.
   - ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/02.png)

### Đạo hàm với Đồ thị Tính toán

- Quy tắc chuỗi giải tích cho biết:
   Nếu `x -> y -> z` (x ảnh hưởng đến y và y ảnh hưởng đến z)
   Khi đó `d(z)/d(x) = d(z)/d(y) * d(y)/d(x)`
- Video minh họa ví dụ lớn.
   - ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/03.png)
- Ta tính đạo hàm trên đồ thị từ phải sang trái sẽ dễ dàng hơn rất nhiều.
- `dvar` có nghĩa là đạo hàm của một biến đầu ra cuối cùng đối với các đại lượng trung gian khác nhau.

### Hồi quy logistic Gradient Descent

- Trong video anh ấy đã thảo luận về các dẫn xuất của gradient ví dụ khá cho một mẫu có hai tính năng `x1` và `x2`.
   - ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/04.png)

### Gradient Descent trên m Ví dụ

- Hãy nói rằng chúng ta có các biến này:

   ```
   Tính năng X1
   Tính năng X2
   W1 Trọng lượng của tính năng đầu tiên.
   W2 Trọng lượng của tính năng thứ hai.
   B Thông số hồi quy logistic.
   M Số ví dụ huấn luyện
   Y(i) Sản lượng dự kiến của i
   ```

- Vì vậy chúng ta có:
   ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/09.png)

- Sau đó từ phải qua trái ta sẽ tính đạo hàm so với kết quả:

   ```
   d(a) = d(l)/d(a) = -(y/a) + ((1-y)/(1-a))
   d(z) = d(l)/d(z) = a - y
   d(W1) = X1 * d(z)
   d(W2) = X2 * d(z)
   d(B) = d(z)
   ```

- Từ những điều trên ta có thể kết luận mã giả hồi quy logistic:

```
 	J = 0; dw1 = 0; dw2 =0; db = 0;                 # Devs.
	w1 = 0; w2 = 0; b=0;							# Weights
	for i = 1 to m
		# Forward pass
		z(i) = W1*x1(i) + W2*x2(i) + b
		a(i) = Sigmoid(z(i))
		J += (Y(i)*log(a(i)) + (1-Y(i))*log(1-a(i)))

		# Backward pass
		dz(i) = a(i) - Y(i)
		dw1 += dz(i) * x1(i)
		dw2 += dz(i) * x2(i)
		db  += dz(i)
	J /= m
	dw1/= m
	dw2/= m
	db/= m

	# Gradient descent
	w1 = w1 - alpha * dw1
	w2 = w2 - alpha * dw2
	b = b - alpha * db
```

- Đoạn mã trên nên chạy lặp đi lặp lại để giảm thiểu lỗi.

- Như vậy sẽ có 2 vòng lặp bên trong để thực hiện hồi quy logistic.

- Vectorization rất quan trọng trong deep learning để giảm vòng lặp. Trong mã cuối cùng, chúng ta có thể tạo toàn bộ vòng lặp trong một bước bằng cách sử dụng vector hóa!

### Vectorization

- Học sâu tỏa sáng khi tập dữ liệu lớn. Tuy nhiên, các vòng lặp for sẽ khiến bạn phải chờ đợi rất nhiều để có kết quả. Đó là lý do tại sao chúng ta cần Vectorization để loại bỏ một số vòng lặp for.
- Chức năng thư viện NumPy (dot) đang sử dụng Vectorization theo mặc định.
- Việc Vectorization có thể được thực hiện trên CPU hoặc GPU dựa trên hoạt động của SIMD. Nhưng nó nhanh hơn trên GPU.
- Bất cứ khi nào có thể tránh vòng lặp for.
- Hầu hết các phương thức thư viện NumPy đều là phiên bản Vectorization.

### Vectorization hồi quy logistic

- Chúng ta sẽ triển khai Hồi quy logistic bằng cách sử dụng một vòng lặp for sau đó không sử dụng bất kỳ vòng lặp for nào.
- Là đầu vào, chúng ta có ma trận `X` và `[Nx, m]` của nó và ma trận `Y` và `[Ny, m]` của nó.
- Sau đó, chúng ta sẽ tính toán tại ví dụ `[z1,z2...zm] = W' * X + [b,b,...b]`. Điều này có thể được viết bằng python như:

    Z = np.dot(W.T,X) + b # Vectorization, sau đó phát sóng, hình dạng Z là (1, m)
    A = 1/1 + np.exp(-Z) # Vectorization, hình A là (1, m)

- Đầu ra Gradient của hồi quy logistic Vectorizing:

   dz = A - Y # Vector hóa, hình dạng dz là (1, m)
   dw = np.dot(X, dz.T) / m # Vectorization, hình dạng dw là (Nx, 1)
   db = dz.sum() / m # Vectorization, hình dz là (1, 1)
   
   ### Ghi chú về Python và NumPy

- Trong NumPy, `obj.sum(axis = 0)` tính tổng các cột trong khi `obj.sum(axis = 1)` tính tổng các hàng.
- Trong NumPy, `obj.reshape(1,4)` thay đổi hình dạng của ma trận bằng cách phát các giá trị.
- Tính toán lại không tốn kém, vì vậy hãy đặt nó ở mọi nơi bạn không chắc chắn về tính toán.
- Phát sóng hoạt động khi bạn thực hiện thao tác ma trận với các ma trận không khớp với thao tác, trong trường hợp này, NumPy tự động làm cho các hình sẵn sàng cho thao tác bằng cách truyền các giá trị.
- Về nguyên tắc chung của phát sóng. Nếu bạn có một ma trận (m,n) và bạn cộng(+) hoặc trừ(-) hoặc nhân(*) hoặc chia(/) với ma trận (1,n), thì điều này sẽ sao chép nó m lần vào một ( m,n) ma trận. Tương tự nếu bạn sử dụng các thao tác đó với ma trận (m , 1), thì thao tác này sẽ sao chép nó n lần vào ma trận (m, n). Và sau đó áp dụng phép cộng, trừ và nhân chia thành phần một cách khôn ngoan.
- Một số thủ thuật để loại bỏ tất cả các lỗi lạ trong mã:
  - Nếu bạn không chỉ định hình dạng của vectơ, nó sẽ có hình dạng `(m,)` và thao tác chuyển đổi sẽ không hoạt động. Bạn phải định hình lại nó thành `(m, 1)`
  - Cố gắng không sử dụng ma trận hạng một trong ANN
  - Đừng ngần ngại sử dụng `assert(a.shape == (5,1))` để kiểm tra xem hình dạng ma trận của bạn có phải là hình dạng được yêu cầu hay không.
  - Nếu bạn đã tìm thấy ma trận hạng một, hãy thử chạy định hình lại trên đó.
- Sổ ghi chép Jupyter / IPython là thư viện rất hữu ích trong python giúp dễ dàng tích hợp mã và tài liệu cùng một lúc. Nó chạy trong trình duyệt và không cần IDE để chạy.
  - Để mở Jupyter Notebook, mở dòng lệnh và gọi: `jupyter-notebook` Phải cài đặt mới dùng được.
- Để tính đạo hàm của Sigmoid:

  ```
  s = sigmoid(x)
  ds = s * (1 - s) # đạo hàm dùng giải tích
  ```

- Để biến hình ảnh của `(chiều rộng, chiều cao, chiều sâu)` thành một vectơ, hãy sử dụng:

  ```
  v = image.reshape(image.shape[0]*image.shape[1]*image.shape[2],1) # định hình lại hình ảnh.
  ```

- Độ dốc gốc hội tụ nhanh hơn sau khi chuẩn hóa ma trận đầu vào.

### Ghi chú chung

- Các bước chính để xây dựng một Neural Network là:
   - Xác định cấu trúc mô hình (chẳng hạn như số lượng tính năng đầu vào và đầu ra)
   - Khởi tạo các tham số của mô hình.
   - Vòng.
     - Tính tổn thất dòng điện (lan truyền thuận)
     - Tính toán gradient hiện tại (lan truyền ngược)
     - Cập nhật thông số (giảm dần độ dốc)
- Tiền xử lý tập dữ liệu là quan trọng.
- Điều chỉnh tốc độ học (là một ví dụ về "siêu tham số") có thể tạo ra sự khác biệt lớn cho thuật toán.
- [kaggle.com](kaggle.com) là một nơi tốt cho các bộ dữ liệu và cuộc thi.
- [Pieter Abbeel](https://www2.eecs.berkeley.edu/Faculty/Homepages/abbeel.html) là một trong những chương trình học tăng cường sâu tốt nhất.

## Mạng lưới thần kinh nông

> Tìm hiểu cách xây dựng mạng nơ-ron với một lớp ẩn, sử dụng lan truyền xuôi và lan truyền ngược.

## Mạng lưới thần kinh nông

> Tìm hiểu cách xây dựng mạng nơ-ron với một lớp ẩn, sử dụng lan truyền xuôi và lan truyền ngược.

### Tổng quan về Mạng nơ-ron

- Trong hồi quy logistic ta có:

  ```
  X1 \
  X2 ==> z = XW + B ==> a = Sigmoid(z) ==> l(a,Y)
  X3 /
  ```

- Trong mạng nơron một lớp ta sẽ có:

  ```
  X1 \
  X2 => z1 = XW1 + B1 => a1 = Sigmoid(z1) => z2 = a1W2 + B2 => a2 = Sigmoid(z2) => l(a2,Y)
  X3 /
  ```

- `X` là vectơ đầu vào `(X1, X2, X3)` và `Y` là biến đầu ra `(1x1)`
- NN là chồng đối tượng hồi quy logistic.

### Biểu diễn mạng nơ-ron

- Chúng ta sẽ định nghĩa các mạng nơ-ron có một lớp ẩn.
- NN chứa các lớp đầu vào, lớp ẩn, lớp đầu ra.
- Lớp ẩn có nghĩa là chúng ta không thể nhìn thấy lớp đó trong tập huấn luyện.
- `a0 = x` (lớp đầu vào)
- `a1` sẽ đại diện cho việc kích hoạt các nơ-ron ẩn.
- `a2` sẽ đại diện cho lớp đầu ra.
- Chúng ta đang nói về NN 2 lớp. Lớp đầu vào không được tính.

### Tính toán đầu ra của Mạng nơ-ron

- Phương trình của các lớp ẩn:
   - ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/05.png)
- Dưới đây là một số thông tin về hình ảnh cuối cùng:
   - `noOfHiddenNeurons = 4`
   - `Nx = 3`
   - Hình dạng của các biến:
     - `W1` là ma trận của lớp ẩn đầu tiên, nó có dạng `(noOfHiddenNeurons,nx)`
     - `b1` là ma trận của lớp ẩn đầu tiên, nó có dạng `(noOfHiddenNeurons,1)`
     - `z1` là kết quả của phương trình `z1 = W1*X + b`, nó có dạng `(noOfHiddenNeurons,1)`
     - `a1` là kết quả của phương trình `a1 = sigmoid(z1)`, nó có dạng `(noOfHiddenNeurons,1)`
     - `W2` là ma trận của lớp ẩn thứ 2, nó có dạng `(1,noOfHiddenNeurons)`
     - `b2` là ma trận của lớp ẩn thứ 2, nó có dạng `(1,1)`
     - `z2` là kết quả của phương trình `z2 = W2*a1 + b`, nó có dạng `(1,1)`
     - `a2` là kết quả của phương trình `a2 = sigmoid(z2)`, nó có dạng `(1,1)`

### Vectơ hóa trên nhiều ví dụ

- Mã giả truyền xuôi cho NN 2 lớp:

```
for i = 1 to m
  z[1, i] = W1*x[i] + b1      # shape of z[1, i] is (noOfHiddenNeurons,1)
  a[1, i] = sigmoid(z[1, i])  # shape of a[1, i] is (noOfHiddenNeurons,1)
  z[2, i] = W2*a[1, i] + b2   # shape of z[2, i] is (1,1)
  a[2, i] = sigmoid(z[2, i])  # shape of a[2, i] is (1,1)
```

- Giả sử chúng ta có `X` trên hình `(Nx,m)`. Vì vậy, mã giả mới:

  ```
  Z1 = W1X + b1 # hình dạng của Z1 (noOfHiddenNeurons,m)
  A1 = sigmoid(Z1) # hình dạng của A1 (noOfHiddenNeurons,m)
  Z2 = W2A1 + b2 # hình dạng của Z2 là (1,m)
  A2 = sigmoid(Z2) # hình dạng của A2 là (1,m)
  ```

- Nếu bạn để ý luôn m là số cột.
- Trong ví dụ trước, chúng ta có thể gọi `X` = `A0`. Vì vậy, bước trước có thể được viết lại thành:

  ```
  Z1 = W1A0 + b1 # hình dạng của Z1 (noOfHiddenNeurons,m)
  A1 = sigmoid(Z1) # hình dạng của A1 (noOfHiddenNeurons,m)
  Z2 = W2A1 + b2 # hình dạng của Z2 là (1,m)
  A2 = sigmoid(Z2) # hình dạng của A2 là (1,m)
  ```

### Chức năng kích hoạt

- Cho đến nay mình đang sử dụng sigmoid, nhưng trong một số trường hợp, các chức năng khác có thể tốt hơn rất nhiều.
- Sigmoid có thể dẫn chúng ta đến vấn đề về độ dốc khi các bản cập nhật quá thấp.
- Phạm vi chức năng kích hoạt sigmoid là [0,1]
  `A = 1 / (1 + np.exp(-z)) # Trong đó z là ma trận đầu vào`
- Phạm vi hàm kích hoạt Tánh là [-1,1] (Phiên bản thay đổi của hàm sigmoid)
  - Trong NumPy, chúng ta có thể triển khai Tanh bằng một trong các phương thức sau:
    `A = (np.exp(z) - np.exp(-z)) / (np.exp(z) + np.exp(-z)) # Trong đó z là ma trận đầu vào`

    Hoặc
    `A = np.tanh(z) # Trong đó z là ma trận đầu vào`
- Hóa ra, kích hoạt tanh thường hoạt động tốt hơn chức năng kích hoạt sigmoid cho các đơn vị ẩn vì giá trị trung bình của đầu ra của nó gần bằng 0 và do đó, nó tập trung dữ liệu tốt hơn cho lớp tiếp theo.
- Nhược điểm của hàm Sigmoid hoặc Tanh là nếu đầu vào quá nhỏ hoặc quá cao, độ dốc sẽ gần bằng 0, điều này sẽ gây ra vấn đề về độ dốc.
- Một trong những hàm kích hoạt phổ biến giải quyết khá tốt gradient chậm là hàm RELU.
  `RELU = max(0,z) # vì vậy nếu z âm thì độ dốc bằng 0 và nếu z dương thì độ dốc vẫn tuyến tính.`
- Vì vậy, đây là một số quy tắc cơ bản để chọn chức năng kích hoạt, nếu phân loại của bạn nằm trong khoảng từ 0 đến 1, hãy sử dụng kích hoạt đầu ra là sigmoid và những cái khác là RELU.
- Chức năng kích hoạt RELU rò rỉ Điểm khác biệt của RELU là nếu đầu vào âm thì độ dốc sẽ rất nhỏ. Nó hoạt động như RELU nhưng hầu hết mọi người sử dụng RELU.
  `Leaky_RELU = max(0,01z,z) # 0,01 có thể là tham số cho thuật toán của bạn.`
- Tại NN bạn sẽ quyết định rất nhiều sự lựa chọn như:
  - Không có lớp ẩn.
  - Không có tế bào thần kinh trong mỗi lớp ẩn.
  - Tỷ lệ học. (Thông số quan trọng nhất)
  - Các chức năng kích hoạt.
  - Và những người khác..
- Hóa ra không có đường hướng dẫn nào cho việc đó. Bạn nên thử tất cả các chức năng kích hoạt chẳng hạn.

### Đạo hàm của hàm kích hoạt

- Nguồn gốc của hàm kích hoạt Sigmoid:

   ```
   g(z) = 1/(1 + np.exp(-z))
   g'(z) = (1 / (1 + np.exp(-z))) * (1 - (1/(1 + np.exp(-z))))
   g'(z) = g(z) * (1 - g(z))
   ```

- Dẫn xuất hàm kích hoạt Tanh:

   ```
   g(z) = (e^z - e^-z) / (e^z + e^-z)
   g'(z) = 1 - np.tanh(z)^2 = 1 - g(z)^2
   ```

- Nguồn gốc hàm kích hoạt RELU:

   ```
   g(z) = np.maximum(0,z)
   g'(z) = { 0 nếu z < 0
             1 nếu z >= 0 }
   ```

- Nguồn gốc của hàm kích hoạt RELU bị rò rỉ:

   ```
   g(z) = np.maximum(0,01 * z, z)
   g'(z) = { 0,01 nếu z < 0
             1 nếu z >= 0 }
   ```

### Gradient descent cho Mạng thần kinh
- Trong phần này chúng ta sẽ có toàn bộ quá trình lan truyền ngược của mạng nơ-ron (Chỉ là các phương trình không có lời giải thích).
- Thuật toán giảm độ dốc:
   - Thông số NN:
     - `n[0] = Nx`
     - `n[1] = NoOfHiddenNeurons`
     - `n[2] = NoOfOutputNeurons = 1`
     - Hình dạng `W1` là `(n[1],n[0])`
     - Hình dạng `b1` là `(n[1],1)`
     - Hình dạng `W2` là `(n[2],n[1])`
     - Hình dạng `b2` là `(n[2],1)`
   - Hàm chi phí `I = I(W1, b1, W2, b2) = (1/m) * Sum(L(Y,A2))`
   - Sau đó Gradient giảm dần:

     ```
     Nói lại:
     Tính các dự đoán (y'[i], i = 0,...m)
     Nhận các công cụ phái sinh: dW1, db1, dW2, db2
     Cập nhật: W1 = W1 - LearningRate * dW1
     b1 = b1 - LearningRate * db1
     W2 = W2 - Tỷ lệ học tập * dW2
     b2 = b2 - LearningRate * db2
     ```

- Truyền thuận:

   ```
   Z1 = W1A0 + b1 # A0 là X
   A1 = g1(Z1)
   Z2 = W2A1 + b2
   A2 = Sigmoid(Z2) # Sigmoid vì đầu ra nằm trong khoảng từ 0 đến 1
   ```

- Lan truyền ngược (dẫn xuất):
   ```
   dZ2 = A2 - Y # đạo hàm của hàm chi phí chúng tôi đã sử dụng * đạo hàm của hàm sigmoid
   dW2 = (dZ2 * A1.T) / m
   db2 = Tổng(dZ2) / m
   dZ1 = (W2.T * dZ2) * g'1(Z1) # tích phần tử (*)
   dW1 = (dZ1 * A0.T) / m # A0 = X
   db1 = Tổng(dZ1) / m
   # Gợi ý có các phép chuyển vị với phép nhân vì để giữ kích thước chính xác
   ```
- Cách chúng tôi rút ra 6 phương trình của lan truyền ngược:
   ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/06.png)

### Khởi tạo ngẫu nhiên

- Trong hồi quy logistic, việc khởi tạo các trọng số một cách ngẫu nhiên là không quan trọng, trong khi trong NN, chúng ta phải khởi tạo chúng một cách ngẫu nhiên.

- Nếu chúng ta khởi tạo tất cả các trọng số bằng 0 trong NN thì sẽ không hoạt động (khởi tạo sai lệch bằng 0 là được):
  - tất cả các đơn vị ẩn sẽ hoàn toàn giống nhau (đối xứng) - tính toán chính xác cùng một chức năng
  - trên mỗi lần lặp giảm dần độ dốc, tất cả các đơn vị ẩn sẽ luôn cập nhật giống nhau

- Để giải quyết vấn đề này, chúng tôi khởi tạo W với một số ngẫu nhiên nhỏ:

  ```
  W1 = np.random.randn((2,2)) * 0,01 # 0,01 để làm cho nó đủ nhỏ
  b1 = np.zeros((2,1)) # có b bằng 0 cũng được, nó sẽ không đưa chúng ta đến bài toán phá vỡ đối xứng
  ```

- Chúng tôi cần các giá trị nhỏ vì trong sigmoid (hoặc tanh), chẳng hạn, nếu trọng lượng quá lớn, bạn có nhiều khả năng kết thúc ngay từ khi bắt đầu đào tạo với các giá trị Z rất lớn. Điều này gây ra tanh hoặc sigmoid của bạn chức năng kích hoạt bị bão hòa, do đó làm chậm quá trình học. Nếu bạn không có bất kỳ chức năng kích hoạt sigmoid hoặc tanh nào trong mạng thần kinh của mình, thì đây không phải là vấn đề.

- Hằng số 0.01 là được đối với mạng 1 lớp ẩn, nhưng nếu NN sâu thì con số này có thể thay đổi nhưng nó sẽ luôn là một con số nhỏ.

## Mạng thần kinh sâu

> Hiểu các tính toán chính làm cơ sở cho học sâu, sử dụng chúng để xây dựng và đào tạo mạng nơ-ron sâu, đồng thời áp dụng vào thị giác máy tính.

### Mạng nơ-ron lớp L sâu

- NN nông là NN có một hoặc hai lớp.
- NN sâu là NN có từ ba lớp trở lên.
- Chúng ta sẽ sử dụng ký hiệu `L` để chỉ số lớp trong một NN.
- `n[l]` là số nơ-ron trong một lớp cụ thể `l`.
- `n[0]` biểu thị số lớp đầu vào nơ-ron. `n[L]` biểu thị số nơ-ron trong lớp đầu ra.
- `g[l]` là hàm kích hoạt.
- `a[l] = g[l](z[l])`
- Trọng số `w[l]` được sử dụng cho `z[l]`
- `x = a[0]`, `a[l] = y'`
- Đây là những ký hiệu chúng tôi sẽ sử dụng cho mạng lưới thần kinh sâu.
- Vì vậy chúng tôi có:
   - Một vectơ `n` của hình dạng `(1, NoOfLayers+1)`
   - Một vectơ `g` của hình dạng `(1, NoOfLayers)`
   - Một danh sách các hình dạng khác nhau `w` dựa trên số lượng tế bào thần kinh trên lớp trước và lớp hiện tại.
   - Một danh sách các hình dạng khác nhau `b` dựa trên số lượng tế bào thần kinh trên lớp hiện tại.

### Truyền bá Chuyển tiếp trong Mạng Sâu (Forward Propagation in a Deep Network)

- Quy tắc chung lan truyền thuận cho một đầu vào:

   ```
   z[l] = W[l]a[l-1] + b[l]
   a[l] = g[l](a[l])
   ```

- Quy tắc chung lan truyền xuôi cho đầu vào `m`:

   ```
   Z[l] = W[l]A[l-1] + B[l]
   A[l] = g[l](A[l])
   ```

- Chúng ta không thể tính toán sự lan truyền về phía trước của toàn bộ lớp mà không có vòng lặp for nên có thể có vòng lặp for ở đây.
- Kích thước của ma trận rất quan trọng, bạn cần phải tìm ra nó.

### Lấy đúng kích thước ma trận của bạn

- Cách tốt nhất để gỡ lỗi kích thước ma trận của bạn là bằng bút chì và giấy.
- Kích thước của `W` là `(n[l],n[l-1])` . Có thể được suy nghĩ từ phải sang trái.
- Kích thước của `b` là `(n[l],1)`
- `dw` có hình dạng giống như `W`, trong khi `db` có hình dạng giống như `b`
- Kích thước của `Z[l],` `A[l]`, `dZ[l]`, và `dA[l]` là `(n[l],m)`

### Tại sao phải biểu diễn sâu?

- Tại sao NN sâu hoạt động tốt, chúng ta sẽ thảo luận câu hỏi này trong phần này.
- Deep NN làm cho quan hệ với dữ liệu từ đơn giản đến phức tạp. Trong mỗi lớp, nó cố gắng tạo mối quan hệ với lớp trước đó. Ví dụ.:
   - 1) Ứng dụng nhận dạng khuôn mặt:
       - Hình ảnh ==> Cạnh ==> Bộ phận khuôn mặt ==> Khuôn mặt ==> khuôn mặt mong muốn
   - 2) Ứng dụng nhận dạng âm thanh:
       - Âm thanh ==> Các tính năng âm thanh cấp thấp như (sss,bb) ==> Âm vị ==> Từ ==> Câu
- Các nhà nghiên cứu thần kinh cho rằng mạng lưới thần kinh sâu "suy nghĩ" giống như bộ não (đơn giản ==> phức tạp)
- Lý thuyết mạch và học sâu:
   - ![]([Hình ảnh/07.png](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/07.png))
- Khi khởi động vào một ứng dụng, đừng khởi động trực tiếp bởi hàng chục lớp ẩn. Hãy thử các giải pháp đơn giản nhất (ví dụ: Hồi quy logistic), sau đó thử mạng nơ-ron nông, v.v.

### Các khối xây dựng của mạng lưới thần kinh sâu

- Truyền xuôi và truyền ngược cho lớp l:
   - ![Untitled](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/10.png)
- Khối NN sâu:
   - ![](https://raw.githubusercontent.com/mbadry1/DeepLearning.ai-Summary/master/1-%20Neural%20Networks%20and%20Deep%20Learning/Images/08.png)

### Forward and Backward Propagation

- Mã giả truyền xuôi cho lớp l:

   ```
   Đầu vào A[l-1]
   Z[l] = W[l]A[l-1] + b[l]
   A[l] = g[l](Z[l])
   Đầu ra A[l], bộ đệm(Z[l])
   ```

- Mã giả lan truyền ngược lớp l:

   ```
   Đầu vào da[l], Bộ nhớ đệm
   dZ[l] = dA[l] * g'[l](Z[l])
   dW[l] = (dZ[l]A[l-1].T) / m
   db[l] = sum(dZ[l])/m # Đừng quên axis=1, keepdims=True
   dA[l-1] = w[l].T * dZ[l] # Phép nhân ở đây là tích vô hướng.
   Đầu ra dA[l-1], dW[l], db[l]
   ```

- Nếu chúng ta đã sử dụng hàm mất mát thì:

   ```
   dA[L] = (-(y/a) + ((1-y)/(1-a)))
   ```

### Tham số so với Siêu tham số

- Các thông số chính của NN là `W` và `b`
- Các tham số Hyper (các tham số điều khiển thuật toán) như:
  - Tỷ lệ học.
  - Số lần lặp.
  - Số lớp ẩn `L`.
  - Số đơn vị ẩn `n`.
  - Lựa chọn các chức năng kích hoạt.
- Bạn phải tự mình thử các giá trị của siêu tham số.
- Trong những ngày đầu của tốc độ học DL và ML thường được gọi là một tham số, nhưng nó thực sự (và bây giờ mọi người gọi nó là) một siêu tham số.
- Trong khóa học tiếp theo, chúng ta sẽ xem cách tối ưu hóa siêu tham số.

### Điều này có liên quan gì đến bộ não

- Phép loại suy "Nó giống như bộ não" đã thực sự trở thành một lời giải thích quá đơn giản.
- Có một sự tương đồng rất đơn giản giữa một đơn vị hậu cần và một tế bào thần kinh duy nhất trong não.
- Không có con người ngày nay hiểu làm thế nào một tế bào thần kinh não người hoạt động.
- Con người ngày nay không biết chính xác có bao nhiêu tế bào thần kinh trên não.
- Học sâu theo quan điểm của Andrew rất tốt ở chỗ học rất linh hoạt, các hàm phức tạp để học ánh xạ X to Y, học ánh xạ đầu vào-đầu ra (học có giám sát).
- Lĩnh vực thị giác máy tính đã lấy cảm hứng từ bộ não con người nhiều hơn một chút so với các lĩnh vực khác cũng áp dụng học sâu.
- NN là một đại diện nhỏ về cách thức hoạt động của bộ não. Mô hình gần nhất của bộ não con người là trong thị giác máy tính (CNN)

## Thêm: Phỏng vấn Ian Goodfellow

- Ian là một trong những nhà nghiên cứu về deep learning nổi tiếng nhất thế giới.
- Ian chủ yếu làm việc với các mô hình thế hệ. Anh ấy là người tạo ra GAN.
- Chúng ta cần ổn định GANs. GAN ổn định có thể trở thành mô hình tổng quát tốt nhất.
- Ian đã viết cuốn sách giáo khoa đầu tiên về phiên bản học sâu hiện đại cùng với Yoshua Bengio và Aaron Courville.
- Ian đã làm việc với [OpenAI.com](https://openai.com/) và Google trên các ứng dụng ML và NN.
- Ian nói với tất cả những ai muốn vào AI phải lấy bằng tiến sĩ. hoặc đăng mã của bạn lên Github và các công ty sẽ tìm thấy bạn.
- Ian nghĩ rằng chúng ta cần bắt đầu dự đoán các vấn đề bảo mật với ML ngay bây giờ và đảm bảo rằng các thuật toán này được bảo mật ngay từ đầu thay vì cố gắng vá nó trong nhiều năm về sau.





<br><br>
<br><br>
Những Ghi chú này được thực hiện bởi [Mahmoud Badry](mailto:mma18@fayoum.edu.eg) @2017
 Nguồn: [Neural Networks and Deep Learning](https://github.com/mbadry1/DeepLearning.ai-Summary/tree/master/1-%20Neural%20Networks%20and%20Deep%20Learning)
