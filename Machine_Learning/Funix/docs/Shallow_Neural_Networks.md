### Mục tiêu của bài viết này:

- Hiểu được hidden units và hidden layers
- Có thể áp dụng một loạt các hàm activation trong một mạng thần kinh
- Xây dựng forward và backward propagation
- Xây dựng và huấn luyện một mạng lưới thần kinh với một lớp ẩn

## Neural Networks Overview
Trong hồi quy logistic, mình đã giới thiệu từ bài trước thì mô hình của nó sẽ như sau:

![A](https://images.viblo.asia/059ac5bf-3301-4f5a-8ed2-1321b61f62ff.png)

Trong trường hợp mạng thần kinh có một lớp ảnh duy nhất thì cấu trúc của nó sẽ như sau:

![S](https://images.viblo.asia/b90c59c3-ba0c-4a57-96ed-c36bc4abab20.png)

## Neural Network Representation
Chúng ta hãy xem xét một đại diện của mạng thần kinh như sau:

![D](https://images.viblo.asia/f278a993-05a6-4725-a77f-f0d802e56cd1.png)

Bạn có thể xác định số lượng các lớp ở trên không ? Nhớ rằng trong khi điếm số lượng lớp của NN (Neural Network), chúng ta không đếm lớp đầu vào. Vì vậy trong hình trên có 2 lớp là một lớp ẩn và một lớp đầu ra.

Lớp đầu tiên được gọi là [0] , lớp thứ hai là [1] và lớp cuối cùng là [2] . Ở đây 'a' là viết tắt của kích hoạt (activation), là các giá trị mà các lớp khác nhau của mạng thần kinh truyền sang lớp tiếp theo. Các tham số tương ứng là $W^{[1]}, b^{[1]}, W^{[2]}, b^{[2]}$

![F](https://images.viblo.asia/13f6a325-d395-4d8e-b589-362dd47b0b48.png)

Đây là một mạng thần kinh đại diện. Tiếp theo chúng ta sẽ xem cách tính đầu ra của mạng thần kinh.

## Computing a Neural Network’s Output

Chúng ta hãy xem xét chi tiết cách mỗi nơ ron của mạng thần kinh hoạt động. Mỗi nơ ron sẽ nhận một đầu vào, thực hiện 1 số phép biến đổi trên chúng (ở đây là tính $Z = W{[T]}x + b$) sau đó áp dụng hàm sigmoid:

![G](https://images.viblo.asia/baa46a6f-1096-4754-a226-6c1fc19edc68.png)

Các bước này sẽ thực hiện trên mỗi tế bào thân kinh. Các phương trình cho lớp ẩn đầu tiên với 4 nơ-ron sẽ là:

![H](https://images.viblo.asia/3551d7c8-df22-42d6-bdcd-66554dd8ca70.png)

Vì vậy, với đầu vào X đã cho, các đầu ra của lớp 1 và 2 sẽ là:

![J](https://images.viblo.asia/9742b40c-2164-4498-bf55-49fccbc2c705.PNG)

Để tính toán các đầu ra này, chúng ta cần chạy một vòng lặp for sẽ tính toán các giá trị này cho từng nơ ron. Nhưng nhớ lại rằng việc sử dụng vòng lặp for sẽ làm cho việc tính toán rất chậm và do đó chúng ta nên tối ưu hóa mã để loại bỏ vòng lặp này và chương trình chạy nó nhanh hơn.

## Vectorizing across multiple examples

Hình thức non-vectorized của đầu ra từ một mạng nơ ron là:

![L](https://images.viblo.asia/8f7b16fe-57b7-4a97-8176-1dc331269f9e.PNG)

Sử dụng vòng lặp, chúng ta tính `z` và giá trị `a` cho từng ví dụ đào tạo riêng biệt. Bây giờ chúng ta sẽ xem làm thế nào nó có thể được vectorized. Tất cả các ví dụ đào tạo sẽ được hợp nhất trong một ma trận X :

![Q](https://images.viblo.asia/abf1a174-41dd-4348-953f-0f4e57ab2840.png)

Khi đó đầu ra theo vectorized sẽ trở thành:

![W](https://images.viblo.asia/acd77a72-949c-40a2-a2bf-4558e612939d.PNG)

Điều này sẽ giảm thời gian tính toán

## Activation Function

Trong khi tính toán đầu ra, một hàm kích hoạt được áp dụng. Việc lựa chọn một hàm kích hoạt ảnh hưởng rất lớn đến hiệu suất của mô hình. Cho đến nay, chúng tôi đã sử dụng hàm kích hoạt sigmoid:

![R](https://images.viblo.asia/a25481a2-221c-4ebf-a34a-abdf176fc2e5.png)

Tuy nhiên, điều này có thể không phải là lựa chọn tốt nhất trong một số trường hợp. Tại sao? Bởi vì ở các cực của đồ thị, đạo hàm sẽ gần bằng 0 và do đó độ dốc giảm dần sẽ cập nhật các tham số rất chậm.

Có các hàm khác có thể thay thế hàm kích hoạt này:

- Tanh

1[O](https://images.viblo.asia/cbaf334a-9f47-489a-be76-09b7c3e121b3.png)

[Shallow Neural Networks](https://viblo.asia/p/shallow-neural-networks-Do7546y0ZM6)
