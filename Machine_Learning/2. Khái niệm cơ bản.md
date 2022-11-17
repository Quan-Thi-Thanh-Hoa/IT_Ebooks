# Những khái niệm cơ bản trong Machine Learning

**Quan sát (Observation):** Là tập dữ liệu đầu vào (input) của bài toán, thường có dạng vector thường được gọi là vector đặc trưng (feature vector) và mỗi xi một đặc trưng (feature).

> Ví dụ: Muốn dự đoán giá nhà dựa vào các dữ liệu quan sát gồm các feature (vị trí nhà, hướng nhà, tình trạng giao thông, cơ sở hạ tầng, giá nhà trung bình,...).

**Nhãn (Label):** Là đầu ra cần dự đoán (với bài toán học có giám sát). Mỗi quan sát sẽ có một nhãn tương ứng trong dữ liệu.

> Ví dụ trên: Label giá nhà có thể là 1 tỷ, 2 tỷ, 2.5 tỷ... hoặc trong một số bài toán với điều kiện nhà như vậy thì có quyết định **Mua** hay **Không mua**. Nhãn có thể mang nhiều dạng nhưng đều có thể chuyển đổi thành một số thực hoặc một vector.

**Tập dữ liệu (dataset):** là tập hợp của các quan sát hay các mẫu dữ liệu và các nhãn có được sử dụng để xây dựng mô hình.

**Mô hình (Model):** là một hàm $f(x)$ hoặc một quy tắc $R$ cho phép ánh xạ dữ liệu quan sát sang một dự đoán đầu ra (có thể là nhãn của dữ liệu hoặc mối quan hệ trong dữ liệu).

**Tham số (parameter):** Là mọt thứ của mô hình được sử dụng để tính toán giá trị đầu ra. Chẳng hạn model là một hàm đa thức bậc hai: $f(x) = ax^2 + bx + c$ thì tham số của mô hình là **a, b, c**. Ngoài ra, còn có một loại tham số đặc biệt khác gọi là __siêu tham số (hyperparameter).__ Đây là một khái niệm mang tính chất khá tương đối chỉ các tham số có dạng cố định và không thay đổi trong quá trình huấn luyện. Đối với hàm đa thức ở trên thì _bậc của đa thức_ có thể được xem là một siêu tham số.

Nguồn: [Teky.vn](https://tek4.vn/khoa-hoc/machine-learning-co-ban/nhung-khai-niem-co-ban-trong-machine-learning)
