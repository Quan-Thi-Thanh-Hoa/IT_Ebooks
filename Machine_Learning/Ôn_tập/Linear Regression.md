# [Machine Learning] Linear Regression và ứng dụng cho bài toán dự đoán điểm Nhập môn Lập trình

Ở đây, mình sẽ áp dụng kiến thức để xây dựng một mô hình máy học để dự đoán điểm cuối kỳ Nhập môn Lập trình, và sẽ được “nghịch” với nó để xem phong cách “học” của máy là như thế nào.

# 1.Linear Regression là gì?

là một trong những thuật toán cơ bản và phổ biến nhất của Supervised Learning (Học có giám sát), trong đó **đầu ra dự đoán là liên tục**. TT này hích hợp để dự đoán các giá trị đầu ra là các đại lượng liên tục như 
- **doanh số hay giá cả** thay vì cố gắng phân loại chúng thành các đại lượng rời rạc như màu sắc và chất liệu của quần áo, 
- hay xác định đối tượng trong một bức ảnh là mèo hay chó, …

> ví dụ: bạn đang có điểm thành phần về các môn như Nhập môn lập trình, OOP, Giải tích,… và điều bạn đang cần là tính ra **điểm trung bình cuối kỳ** của mình. 
> - Bạn sẽ tính được chứ? Bạn chỉ cần áp công thức tính điểm trung bình vào là ra. 
> - Tiếp tục, bạn lại muốn khảo sát, thống kê lại xem điểm thi giữa kỳ Nhập môn lập trình ảnh hưởng như thế nào đến điểm cuối kỳ của các bạn trong lớp, bạn muốn xác định xem quan hệ giữa điểm thành phần và điểm cuối kỳ thì phải làm sao? 

Trong Linear Regression chúng ta sẽ gặp hai loại bài toán:
- **Univariate Linear Regression (hồi quy tuyến tính đơn biến)** chính là mối quan hệ giữa hai biến số liên tục trên trục hoành x và trên trục tung y. Phương trình hồi quy tuyến tính đơn biến có dạng như phương trình đường thẳng y=ax+b với x là biến độc lập và y là biến phụ thuộc vào x.
- Đối với **Hồi quy tuyến tính đa biến**, bạn có thể hiểu một cách đơn giản là sẽ có nhiều biến độc lập x_1, x_2, …, x_n và nhiều hệ số a_1, a_2, …, a_n thay vì chỉ một biến x duy nhất.

# 2. Một vài ký hiệu cần lưu ý và cách xác định input và output của bài toán.

Trong **supervised learning (học có giám sát)**, chúng ta có một bộ dữ liệu và bộ dữ liệu này gọi là **training set (tập huấn luyện)**. 

Giả sử chúng ta có bộ dữ liệu thống kê điểm giữa kỳ và điểm cuối kỳ trong Nhập môn lập trình. Khi đó, với bài toán hồi quy đơn biến này, cần tìm ra một mô hình nhận vào input là điểm giữa kỳ và output ra dự đoán điểm cuối kỳ hợp lí nhất dựa trên mối quan hệ giữa hai cột điểm mà mô hình đó tìm được.

|Điểm giữa kỳ |	Điểm cuối kỳ |
|-------------|--------------|
|    4.00	    |     3.98     |
|    6.00	    |     5.5      |
|    8.75     |   	7.8      |
|    6.70     |	    5.9      |
|    …	      |     …        |
|    7.70     |    	8.6      |

Bảng 1: Thống kê điểm NMLT của sinh viên trong một lớp.

Thống nhất sử dụng một vài ký hiệu: 

- $m$: Đại diện số lượng các training example (mẫu huấn luyện). 
> - Giả  sử, chúng ta có 40 dòng điểm cuối kỳ khác nhau được thu thập dựa trên điểm giữa kỳ tương ứng. Như vậy, ta có 40 mẫu huấn luyện và m bằng 40. 
- $x$: **input variable (biến đầu vào)** cũng thường được gọi là các feature (đặc trưng). Trong hồi quy đa biến, x là một vector nhưng trong ví dụ này, x là số điểm đánh giá trong nửa học kỳ đầu – là một con số trong hồi quy đơn biến.
- $y$: Để ký hiệu **các biến đầu ra hay các biến mục tiêu**, ở đây là điểm cuối kỳ tương ứng.
- $(x,y)$: đại diện một mẫu huấn luyện – training example. 
- $x^(i),y^(i)$: dùng để chỉ một **mẫu huấn luyện** cụ thể. 
> - Giả sử, với i=3 tương ứng ta có điểm dữ liệu $x^(3),y^(3)$: Số điểm cuối kỳ của bạn có thể là bao nhiêu khi điểm giữa kỳ là 8.75? Dựa vào bảng số liệu trên, tại $y^(3)$, kết quả dự đoán đạt giá trị là 7.8.

Chúng ta đã học phương trình đường thẳng $y = ax + b$ ở bậc trung học phổ thông và hàm h – hypothesis (giả thuyết) cũng được biểu diễn tương tự cho mô hình hồi quy tuyến tính đơn biến. Nó cũng sẽ lấy giá trị đầu vào là x và cho ra kết quả đầu ra là y nhưng chỉ thay đổi các thông số a và b thành $θ_0=b$ và $θ_1=a$.

Khi đó về mặt toán học, $h$ là một ánh xạ từ $x$ sang $y$:

$y = h(x) = h_θ(x) = b + ax = θ_0 + θ_1x$

# 3. Bài toán dự đoán điểm trung bình Nhập môn lập trình 

Đi sâu hơn về việc giải quyết các vấn đề hồi quy đơn biến. Nhìn vào các training example (mẫu huấn luyện) được đưa ra trong hình dưới đây.

![](https://lh5.googleusercontent.com/ybiNVpTWs3tohdBFC41JdDw710bBRYLG2PiE7N6rj_Wvnl4MwXdqtFS-203r74azwY5muQpWxD-NULTyB9HuBVkuH2yZEjMQKTnPnG3IOW_36in9YuUKg_vSrDjcUg)

Hình 1

Điều gì sẽ xảy ra khi bạn cần ước lượng số điểm chính xác nhất khi đạt 7.00 điểm giữa kỳ từ thông tin trên? Hướng tiếp cận đơn giản nhất là tìm một đường thẳng (*) phù hợp với  tập dữ liệu và vẽ một đường thẳng từ vị trí 7 điểm trên trục x cho đến khi nó chạm vào đường thẳng(*) vừa tìm?

![](https://lh5.googleusercontent.com/UuxZ_aj6CAQzd27lT5yWTOnqQlx6XxtuZP86KC9lanFbbiulrZR_QC1KM9JuauU0dbFqYYZ924RQYrG_fD0jFW76CgFIUe_fDAugaOlwss6fuHgO5r70FjTCTqcoxA)

Hình 2

Từ hai mẫu (4.00, 3.98) và (6.00, 5.5), ta vẽ được đường thẳng màu đỏ và từ đó tìm được hai giá trị θ_0 và θ_1 lần lượt là 0.76 và 0.94 . Bây giờ, chúng ta có thể sử dụng hàm giả thuyết để dự đoán điểm cuối kỳ dựa trên điểm giữa kỳ tương ứng với giá trị 7.00 như sau:

$h(x) = 0.76x + 0.94 = 0.76 ∗ 7 + 0.94 = 6.26$ điểm – giá trị ước tính tương ứng với đường thẳng này. 

Tuy nhiên, trong thực tế các bộ dữ liệu đưa vào huấn luyện mô hình nhiều hơn gấp trăm, gấp ngàn lần và số lượng các đặc trưng cũng chênh lệch đáng kể, việc xác định hàm tuyến tính trở nên khó khăn hơn. Sự xuất hiện của các vấn đề trên là tiền đề để máy học ra đời, tạo ra nhiều thuật toán phục vụ cho mọi người như áp dụng thuật toán hồi quy tuyến tính và SVM (Support Vector Machine) trong phân tích chứng khoán hay nhận dạng giọng nói bằng mô hình Markov, …

Hàm giả thuyết ở trên được xây dựng tốt hay chưa? Làm sao để hàm đó trở nên phù hợp nhất có thể? Làm thế nào bạn nhận định được điều đó? Nhờ đó hàm mất mát được tạo ra, hàm sẽ giúp bạn tính khoảng cách giữa kết quả mà hàm giả thuyết h dự đoán được so với giá trị thực sự mà ta quan sát thấy.

![](http://tutorials.aiclub.cs.uit.edu.vn/wp-content/uploads/2021/04/1-3.png)

Hình 3: Xây dựng hàm mất mát

Khi bạn có giá trị dự đoán là 6.26 và giá trị thực là 6.00 chúng có ý nghĩa gì? Hàm mất mát sẽ cho bạn biết sự chênh lệch giữa thực tế và giả thuyết và khi giá trị hàm này càng nhỏ, dự đoán của bạn lại càng chính xác và càng phù hợp! Bạn có mong muốn hàm mất mát đưa ra giá trị nhỏ nhất không? Đối với hồi quy tuyến tính, bạn có thể tính bình phương độ sai lệch để đánh giá sự chênh lệch giữa giá trị đưa ra bởi hàm giả thuyết và giá trị thực tế  đo đạc được:

![](https://raw.githubusercontent.com/Quan-Thi-Thanh-Hoa/IT_Ebooks/main/Machine_Learning/%C3%94n_t%E1%BA%ADp/h%C3%A0m%20m%E1%BA%A5t%20m%C3%A1t.png)

Dưới đây là demo code của hàm mất mát của bài toán tính điểm cuối kỳ:

```
def loss_univariate(X, y, theta_0, theta_1):
     h = theta_0 + theta_1 * X
     m = len(X)
     loss = 1/(2*m) * np.sum((y - h) ** 2)
     return loss
```
Từ mô hình dữ liệu hình 1, ta thu được hàm giả thuyết từ điểm giữa kỳ sang điểm cuối kỳ :

$h(x) = cuoiky = 0

[Nguồn](http://tutorials.aiclub.cs.uit.edu.vn/index.php/2021/04/24/linear-regression/)
