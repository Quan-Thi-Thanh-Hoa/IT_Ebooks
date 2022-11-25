# Vectorization Implementation in Machine Learning
Trong lĩnh vực máy học, những người chơi nâng cao có nhu cầu viết hàm chi phí hoặc thuật toán tối ưu hóa của riêng họ để đạt được một mô hình tùy chỉnh hơn, chứ không chỉ sử dụng các thư viện máy học hiện có. Để tận dụng tối đa sức mạnh tính toán của các máy tính ngày nay, công nghệ triển khai thuật toán tiên tiến nhất là véc tơ hóa tất cả các phép tính. Điều này cho phép bạn đạt được tính toán song song, chẳng hạn như sử dụng hoàn toàn bộ xử lý GPU. Trong bài đăng này, việc triển khai vector hóa học máy được giới thiệu. Tất cả mã được sử dụng trong bài đăng này có thể được tìm thấy trong github của tôi.

## Điều kiện tiên quyết: Mảng Numpy

Công cụ quan trọng nhất mà chúng ta sẽ sử dụng trong quá trình vector hóa này là mảng có nhiều mảng. Lưu ý rằng, chúng tôi không sử dụng ma trận numpy vì ma trận numpy hoàn toàn là 2 chiều. Trên thực tế, ma trận có nhiều mảng là một tập hợp con của mảng có nhiều mảng. Vì vậy, để thuận tiện, mình sẽ sử dụng mảng có nhiều mảng. Dưới đây là một bài đánh giá về số học mảng numpy để theo dõi tốt hơn các nội dung sau. Đây là cách **định nghĩa mảng numpy**:

```
# import numpy
import numpy as np
# define two numpy arrays
a = np.array([[1,2],[3,4]])
b = np.array([[1,1],[1,1]])
print(a)
>>> array([[1, 2],
           [3, 4]])
print(b)
>>> array([[1, 1],
           [1, 1]])
```

## Numpy Array Addition

```
# addition
print(a + b)
>>> array([[2, 3],
           [4, 5]])
```

## Numpy Array Subtraction

```
# substraction
print(a - b)
>>> array([[0, 1],
           [2, 3]])
```

## Phép nhân mảng Numpy

Lưu ý rằng nếu sử dụng trực tiếp phép nhân '*', điều này khác với phép nhân ma trận được gọi là tích vô hướng. Các phép toán '*' giữa hai mảng chỉ là nhân các phần tử ở cùng một vị trí.

```
# multiplication: 
print(a * b)
>>> array([[1, 2],
          [3, 4]])
```

## numpy.dot(): cung cấp một hàm để thực hiện tích vô hướng của hai mảng

Chúng tôi sử dụng hàm numpy dot để đạt được phép nhân ma trận. Một cách thuận tiện là chỉ cần sử dụng biểu tượng '@', nó hoạt động chính xác theo cùng một cách.

```
# matrix multiplication
print(np.dot(a,b))
>>> array([[1, 2],
          [3, 4]])
# matrix product alternative
print(a@b)
>>> array([[3, 3],
          [7, 7]])
```

## Kích thước mảng Numpy

Ở đây chúng tôi hiển thị hai ví dụ minh họa cách thứ nguyên hoạt động trong mảng có nhiều mảng. Lưu ý rằng, trong trường hợp đầu tiên, nó là một mảng có một hàng ba cột, trong khi ở trường hợp thứ hai, nó là một mảng có ba hàng nhưng một cột.

```
# numpy array with one row
a =  np.array([1,2,3])
print(a.shape)
>>> (3,)
# numpy array with three rows
b = np.array([[1],[2],[3]])
print(b.shape)
>>> (3, 1)
```

## Lập chỉ mục và cắt mảng Numpy

Đối với mảng 2D numpy, khi chúng ta cắt một phần tử trong một mảng được ký hiệu là A, chúng ta có thể sử dụng A[i, j] trong đó i là chỉ số hàng và j là chỉ số cột. Nếu muốn chọn cả hàng i dùng A[i, :], tương tự để chọn cả cột j dùng A[:,j].

```
# Define an 3x3 2d array
a = np.array([[1,2,3],[4,5,6],[7,8,9]])
print(a)
>>> array([[1, 2, 3],
          [4, 5, 6],
          [7, 8, 9]])
# select first element in the array
print(a[0,0])
>>> 1
# select first row of the array
print(a[0,:])
>>> array([1, 2, 3])
# select second coulumn of the array
print(a[:,1])
>>> array([2, 5, 8])
```

## Điều kiện tiên quyết:

Hàm chi phí hồi quy tuyến tính. Trong phần này, chúng ta sẽ xem lại một số khái niệm và biểu thức toán học của hồi quy tuyến tính. Vì chúng ta cần sử dụng các công thức này để đạt được thuật toán giảm độ dốc trong phần tiếp theo để xem cách thực hiện vector hóa.

![A](https://miro.medium.com/max/1400/1*JJI71Cg0upbdSoxePCH_JA.png)

### Giả thuyết về hồi quy tuyến tính được định nghĩa là:

![R](https://miro.medium.com/max/640/1*k-sttEqbKIOSlAas3C36CA.png)

### Hàm chi phí của hồi quy tuyến tính được định nghĩa là:

![E](https://miro.medium.com/max/630/1*E-iWjE3o9luiVapwzYkR7w.png)

### Đạo hàm của hàm chi phí cho mỗi θ được định nghĩa là:

![A](https://miro.medium.com/max/640/1*vYspf1L6Omqh91nEdHsgEw.png)

### Trong mỗi lần lặp lại độ dốc giảm dần, chúng tôi cập nhật tất cả θ bằng phương trình sau:

![D](https://miro.medium.com/max/640/1*CkcmVCUKmbA-qUn7y8srNQ.png)

## Bộ dữ liệu

Bộ dữ liệu chúng tôi sử dụng là 'Nhà ở Boston' từ Kho lưu trữ công suất máy UCI. Nó đã sử dụng các đặc điểm như quy mô diện tích nhà, năm xây dựng, v.v. để dự đoán giá nhà ở khu vực Boston. Đây là những gì dữ liệu trông giống như:

![E](https://miro.medium.com/max/828/1*7rfGRAy3pTCmS8mOaoCFZg.png)

Tập dữ liệu của chúng tôi có 506 mục nhập, chúng tôi ký hiệu nó là số lượng mục nhập là m. Số lượng tính năng là n=14 bao gồm cả tính năng chặn mà mình khởi tạo dưới dạng tất cả các tính năng. Xem bên dưới:

```
# Insert X0 Column
Xd = df.drop(columns=['MEDV'])
Xd.insert(0, 'X0', 1)
Xd.head()
```

![A](https://miro.medium.com/max/828/1*nwsDpE1uXYtu5qWVe6_Ckw.png)

```
# numpy array format
X = Xd.values
y = df.MEDV.values
# sample size
m = len(df.index)
print(m)
>>> 506
# number of features
n = X.shape[1]
print(n)
>>> 14
```

## Đối với vòng lặp V.S. Vector hóa

Trong phần này, mình thực hiện từng bước so sánh vòng lặp for và phương pháp véc tơ hóa bằng cách áp dụng thuật toán giảm độ dốc cho hồi quy tuyến tính. Mình so sánh thời gian chạy cho mỗi lần thực hiện các công thức trong phần hồi quy tuyến tính.

Mình khởi tạo tất cả các thetas dưới dạng:

```
# Initialize theta
theta = np.ones(n)
print(theta)
>>> array([1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.])
```

## Thực hiện giả thuyết: 

Cho vòng lặp để đạt được hàm giả định của hồi quy tuyến tính, nếu chúng ta sử dụng vòng lặp for, nó có thể đạt được bằng mã sau:

```
# hypothesis for the first sample
hypo = 0
for j in range(n):
    hypo += theta[j]*X[0,j]
```

Để có được giả thuyết cho từng mẫu, chúng ta cần một danh sách để lưu trữ nó và một vòng lặp for khác để lặp lại trên tất cả các mẫu:

```
%%time
# hypothesis for all the samples
all_hypo = []
for i in range(m):
    hypo_i = 0
    for j in range(n):
        hypo_i += theta[j]*X[i,j]
    all_hypo.append(hypo_i)
>>> Wall time: 4 ms
```

Chúng ta có thể thấy thời gian chạy là 4 ms, không quá điên rồ vì việc triển khai này đủ đơn giản và tập dữ liệu nhỏ.

![A](https://miro.medium.com/max/492/1*9qYXZjDFT8fynt9Uy-figQ.png)

Vectorization giả thuyết của từng mẫu có thể được véc tơ hóa bằng công thức sau:

![A](https://miro.medium.com/max/640/1*K6bwmo5ZA00aQau-_S4ryg.png)

Để đạt được giả thuyết cho tất cả các mẫu dưới dạng danh sách, chúng tôi sử dụng tích dấu chấm mảng sau:

1[A](https://miro.medium.com/max/640/1*U4W4RljYFmJQVsLi4YVozw.png)

Trình bày mã khá dễ dàng và rõ ràng:

```
%%time
# matrix format
hypo = X@theta
>>> Wall time: 0 ns
```

Chúng ta có thể thấy rằng nó cần một khoảng thời gian rất nhỏ để tính toán và thậm chí không thể hiển thị được. Kết quả tính toán được hiển thị như dưới đây. So sánh với kết quả của vòng lặp for, chúng ta có thể thấy chúng ta thu được kết quả hoàn toàn giống nhau.

![S](https://miro.medium.com/max/828/1*dp0pPCju7Pkpenc1de3xgA.png)

### Hàm chi phí Thực hiện:

Cho vòng lặp dựa trên kết quả mình thu được từ giả thuyết, mình cần một vòng lặp khác để lặp lại tất cả các mẫu để tính hàm chi phí.

```
%%time
# cost function
cost = 0
for i in range(m):
    hypo_i = 0
    for j in range(n):
        hypo_i += theta[j]*X[i,j]
    cost_i = (hypo_i - y[i])**2
    cost += cost_i
cost = (1/(2*m))*cost
>>> Wall time: 4 ms
```

```
print(cost)
>>> 1.399752908228425
```

### Hàm chi phí Thực hiện:

Vectorization dựa trên việc véc tơ hóa giả thuyết, mình có thể dễ dàng véc tơ hóa hàm chi phí thành:

![D](https://miro.medium.com/max/640/1*rZjirMxeNnyJvziPsOv6Xw.png)

```
%%time
# cost function
cost = (1/(2*m))*np.transpose((X@theta - y))@(X@theta - y)
>>> Wall time: 0 ns
```

Kết quả tính được giống với kết quả của vòng lặp for:

```
print(cost)
>>> 1.3997529082284244
```

### Thực hiện phái sinh: 

Đối với vòng lặp tính đạo hàm của hàm chi phí với một θ xác định được mã hóa như sau:

```
dev_sum = 0
for i in range(m):
    hypo_i = 0
    for j in range(n):
        hypo_i += theta[j]*X[i,j]
    dev_i = (hypo_i - y[i])*X[i,k]
    dev_sum += dev_i
dev_sum = (1/m)*dev_sum
```

Để tính đạo hàm cho tất cả θ và xuất ra một danh sách, chúng ta cần một vòng lặp for khác lặp lại trên tất cả các cột:

```
%%time
# derivation
dev_list = []
for k in range(n):
    dev_sum = 0
    for i in range(m):
        hypo_i = 0
        for j in range(n):
            hypo_i += theta[j]*X[i,j]
        dev_i = (hypo_i - y[i])*X[i,k]
        dev_sum += dev_i
    dev_sum = (1/m)*dev_sum
    
    dev_list.append(dev_sum)
>>> Wall time: 47 ms
```
Thời gian chạy là 47 mili giây, vì mình có nhiều vòng lặp hơn nên chênh lệch chi phí thời gian của vòng lặp for và vector hóa bắt đầu trở nên đáng kể.

```
print(dev_list)
>>> [0.9999999999999983,
 0.07814620360307895,
 -0.11042922261438312,
 0.2620302340552936,
 0.05504439083525137,
 0.23892542562534522,
 -0.06454255823702795,
 0.2611634394125097,
 -0.1453677181065729,
 0.43106386997897883,
 0.38303455280215737,
 0.16591512402899725,
 -0.09920797306076046,
 0.1835280968258358]
 ```
 
 ### Thực hiện phái sinh (Derivation Implementation):

Đạo hàm của hàm chi phí liên quan đến từng θ có thể được véc tơ hóa thành:

![R](https://miro.medium.com/max/566/1*LirPy3hWR--o3bCXkZzsVQ.png)

![R](https://miro.medium.com/max/566/1*TYSV4TecQ9DgSZ_sAQD1mw.png)

```
%%time
dev = (1/m)*np.transpose(X)@(X@theta - y)
>>> Wall time: 999 µs
```

So sánh trực tiếp là 999 μs vs. 47 ms. Đây là kết quả tính toán vector hóa:

```
print(dev)
array([ 1.        ,  0.0781462 , -0.11042922,  0.26203023,  0.05504439, 0.23892543, -0.06454256,  0.26116344, -0.14536772,  0.43106387, 0.38303455,  0.16591512, -0.09920797,  0.1835281 ])
```

Một lần nữa, kết quả là như nhau đối với hai phương pháp.

### Tổng hợp mọi thứ lại với nhau:

Tối ưu hóa trong phần này, mình sử dụng tất cả các triển khai mà mình đã phát triển trước đó và viết một phép lặp giảm dần độ dốc để so sánh hai phương pháp.

### Gradient Descent: 

Cho vòng lặp để đạt được kết quả tối ưu hóa gốc, mình đặt thời gian lặp lại là 100 nghìn. Mình cần bốn vòng for lồng nhau để đạt được thuật toán giảm độ dốc. Tỷ lệ học tập được đặt là 0,0005 và thetas được khởi tạo là tất cả. Mã được hiển thị như dưới đây:

```
%%time
a = 0.0005
theta = np.ones(n)
cost_list = []
for itr in range(100000):
    
    dev_list = []
    for k in range(n):
        dev_sum = 0
        for i in range(m):
            hypo_i = 0
            for j in range(n):
                hypo_i += theta[j]*X[i,j]
            dev_i = (hypo_i - y[i])*X[i,k]
            dev_sum += dev_i
        dev_sum = (1/m)*dev_sum
dev_list.append(dev_sum)
    
    theta = theta - a*np.array(dev_list)
    
    cost_val = cost_loop(theta)
    
    cost_list.append(cost_val)
>>> Wall time: 1h 15min 58s
```

Tổng thời gian chạy là 1 giờ 15 phút. Sau đây là chi phí tối thiểu mình thu được. Mình cũng cung cấp một biểu đồ cho thấy hàm chi phí thay đổi theo các lần lặp lại.

```
print(cost_val)
>>> 0.017663350184258856
```

![A](https://miro.medium.com/max/640/1*ig-sjIZWST1wIztqMEByig.png)

```
%%time
a = 0.0005
theta = np.ones(n)
cost_list = []
for i in range(100000):
    
    theta = theta - a*(1/m)*np.transpose(X)@(X@theta - y)
           
    cost_val = cost(theta)
    cost_list.append(cost_val)
>>> Wall time: 1.75 s
```

Phương pháp vectorized có giá trị hàm chi phí tối thiểu như dưới đây. Một lần nữa, chi phí thay đổi đối với các lần lặp lại được cung cấp:

```
print(cost_val)
>>> 0.017663350184258835
```

![R](https://miro.medium.com/max/640/1*fWSNMlU60DZbTrcbGC-MtA.png)

Chúng ta có thể thấy giá trị chi phí tối thiểu của hai phương pháp gần như hoàn toàn giống nhau. Nhưng thời gian thực hiện thuật toán là 1,75 giây khi sử dụng vector hóa so với 1 giờ và 15 phút khi sử dụng vòng lặp for.

# Kết luận

Đây là một biểu đồ cho thấy sự khác biệt về thời gian chạy của hai phương pháp thực hiện cùng một thuật toán và sử dụng chính xác cùng một tốc độ học tập và các giá trị θ ban đầu. Hai cách tiếp cận đạt được độ chính xác như nhau. Tuy nhiên, phương pháp véc tơ hóa tốn 1,75 giây trong khi vòng lặp for tốn 4558 giây. Phương pháp vector hóa nhanh hơn 2600 lần so với phương pháp vòng lặp for.

![G](https://miro.medium.com/max/720/1*sEJko2YfX0oINarE3sZLVQ.png)

Độ phức tạp thời gian của phương pháp vector hóa là O(s), trong đó s là số lần lặp lại. Ngược lại, độ phức tạp thời gian tiếp cận vòng lặp for là O(s*n*m*n), trong đó s là số lần lặp lại, m là số mẫu của tập dữ liệu, n là số tính năng của tập dữ liệu. Trong trường hợp này, tập dữ liệu của mình đủ nhỏ với m=506 và n=14, tuy nhiên, mình đã quan sát thấy sự khác biệt lớn về độ phức tạp của thời gian. Hình ảnh cho dữ liệu lớn, sự khác biệt này sẽ lớn như thế nào. Vì máy tính và GPU của hiện tại được tạo thành từ hàng nghìn 'lõi' và thậm chí mình có thể có nhiều GPU hoặc sử dụng một cụm máy tính, mình cần tận dụng tốt sức mạnh tính toán này. Và cách thực hiện thuật toán của bạn bằng tính toán song song. Do đó, sử dụng vector hóa trong thuật toán nghiêng máy của mình là chìa khóa để tăng cường thuật toán của bạn và giúp bạn tiết kiệm một lượng lớn thời gian đào tạo. Vectorization sẽ là một cách tiếp cận tuyệt vời mà mình cần xem xét và đáng để dành thời gian.
