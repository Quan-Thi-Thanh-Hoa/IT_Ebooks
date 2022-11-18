# Lương càng cao sẽ càng hạnh phúc? Ví dụ đầu tiên về Machine Learning

## **Bài toán**

Sau nhiều năm hoạt động, một công ty A nhận thấy rằng nhân viên của mình có tỷ lệ bỏ việc khá nhiều và cảm thấy mức độ hài lòng trong công việc của nhân viên là không cao. Trưởng phòng nhân sự đề ra một giả thiết rwafng có thể đo lương nhân viên trong công ty quá thấp dẫn tới mức độ hài lòng với công việc thấp và đề xuất muốn xác định thang lương thưởng mới phù hợp để tăng sự hài lòng cho nhân viên. Để tiến hành khảo sát, phòng nhân sự thống kê lương của nhân viên và đưa nhân viên các phiếu điều tra nặc danh để đánh giá mức độ hài lòng của họ với công việc. Mức độ hài lòng này đượg đánh giá thang điểm từ 1 đến 100 tương ywsng với mưc độ hài lòng của nhân viên đối với công việc. Sau khi thu thập, dữ liệu được tương ứng được đưa ra trong hình vẽ sau:
![VD](https://tek4.vn/public_files/5f6a8ff5-f44c-4588-962c-ce0fb1860fce)
Trong bài toán này, chúng ta thấy rằng: nhiệm vụ T của chúng ta ở đây là dự đoán mức độ hài lòng của nhân viên dựa trên mức lương, đây là một bài toán hồi quy. Trải nghiệm E là khảo sát về mức lương và mức độ hài lòng tương ứng được cho trong Hình vẽ trên, và độ đo P ở đây là dự đoán sai lệch nhỏ nhất. Tức là từ những dữ liệu E đã cho làm thế nào để xây dựng được một mô hình hồi quy dự đoán mức độ hài lòng với công việc theo mức lương sao cho kết quả dự đoán sai lệch ít nhất với thực tế.

**Một số lưu ý**
Đầu tiên, khi nhìn vào bảng dữ liệu ta thấy rằng dữ liệu được phân bố với một chút nhiễu. Do đó, kể cả khi chúng ta có tìm được một quy luật biểu thị quan hệ của dữ liệu này (chẳng hạn mức độ hài lòng tỷ lệ thuận với mức lương) thì quy luật này cũng không thể đúng với 100% dữ liệu (với dữ liệu chưa được quan sát). Điều này đúng với mọi bài toán mchine learning trên thực tế, bởi nhiễu là thứ luôn luôn tồn tại trong dữ liệu và việc dựu đoán một mô hình đúng với 100% dữ liệu thực tế là điều không thể. Chúng ta chỉ có thể làm cho nó đúng 100% trên dữ liệu huấn luyện bằng cách tìm một hàm đa thức xấp xỉ đi qua toàn bọ dữ liệu, nhưng đây không phả ilaf điều chúng ta cần trong machine learning mà đó là công việc của giái tích học. Với machine learning chúng ta muốn xây dựng một mô hình có thể dự đoán được các giá trị chưa được quan sát chứ khonog phải là nhớ toàn bộ dữ liệu (học vẹt) nhưng lại làm sai toét trên dữ liệu chưa thấy.

Về cơ bản, chúng ta nhắc lại câu nói của nhà toán học và thống kê học nổi tiếng `Georrge E. P. Box` "tất cả các mô hình đều sai, nhưng một số thì hữu dụng".

Và mục tiêu của machine learning là tìm ra các mô hình "hữu dụng" đủ tốt này chứ không phải là một mô hình "hoàn hảo" trên toàn bộ dữ liệu huấn luyện.

Học máy chủ yếu dựa trên số liệu thống kê. Để máy có thể học được, chúng ta phải cung cấp cho nó các mẫu ngẫu nhiên có ý nghĩa thống kê làm dữ liệu chuẩn để huaastn luyện. Ở đây chúng ta có 2 khái cạnh cần quan tâm đó là tính "ngẫu nhiên" có nghĩa là nó không bị điều khiển hoặc can thiệp và thứ hai đó là nó phải có ý nghĩa thông kê, tứ là có thể đại diện được cho toàn bộ phân phối trên thực tế của dữ liệu trong tbafi toán. Ví dụ: việc cố gắng dự đoán sự hài lòng  của công ty chỉ dựa trên dữ liệu từ ban quyarn lý cấp trên có thể dễ dẫn đến sai sót bởi duwxl iệu từ ban qunarn lý không thể đjai diện cho toàn bộ cac nhân viên cotrn gcoong ty. Ngoài ra, nếu tập huấn luyện quá nhỏ, thì theo luật số lớn chúng ta cũng sẽ không học được đầy đủ quan hệ trong dữ liệu và thậm chí có thể đưa ra các kết luận không chính xác. Chẳng hạn chỉ lấy ý kiến từ một số thành viên ngẫu nhiên (khoảng 10 người) thì kết quả dự đoán cũng có thể bị thiên lệch hoặc không chính xác.

**Xây dựng mô hình dự đoán mức độ hài lòng với công việc dựa trên mức lương**

Đầu tiên, chúng ta thấy rằng, từ dữ liệu, chúng ta có thể dự đoán rằng mức lương có tỷ lệ thuận với mức độ hài lòng trong công việc. Như vậy, chúng ta sẽ cố gắng tìm ra một quan hệ tuyến tính để dự đoán mức độ hài lòng với công việc thông qua lương. Gọi $x$ là mức lương mà nhân viên được nhận và $y$ là mức độ hài lòng với công việc của anh ta. Mục tiêu của chúng ta là tìm được một hàm dự đoán $y = f(x)$ để tính được mức độ hài lòng trong công việc của nhân viên theo mức lương. Như nhận xét ở trên, giả sử rằng hàm $f$ có dạn tuyến tính, tức là: 
$f(x) = m_1 \times x + m_0$

Khi đó, mục tiêu của chúng ta là phải tìm được giá trị $m_1$ và $m_0$ đủ tốt để dự đoán.

Đây là mục tiêu của machine learning hay cụ thể hơn là các mô hình hồi quy. Tuy nhiên, tạm thời chúng ta chưa quan tâm đến các kiến thức cao siêu ở đây và cũng chưa biết làm thế nào để xây dựng một mô hình hồi quy tốt. Thế thì, chúng ta đầu tiên giả sử khởi tạo một giá trị bất kỳ cho $m_1$ và $m_0$, giả sử, $m_1 = 0.2$ và $m_0 = 10$, ta có:
$f(x) = 0.2 \times x + 12$
![VD](https://tek4.vn/public_files/f0a6f668-bec8-4e03-97ea-6f74b57fea33)

Nhìn có vẻ khá lệch. Và nếu chúng ta sử dụng mô hình này để dự đoán mức độ hài lòng của một nhân viên có mức lương 60 triệu đồng thì chúng ta sẽ thu được mức độ hài lòng của anh ta là 27 (tương đối thấp), trong khi nhìn vào dữ liệu chúng ta thấy rằng với mức lương này thì mức độ hài lòng ít nhất cũng phải lớn gấp đôi.

Kết quả dự đoán khá tệ và mô hình không đủ tốt. Nếu chúng ta tính trung bình các giá trị sai lệch của dự đoán so với thực tế của toàn bộ dữ liệu thì nó sẽ cho một con số rất lớn.

Do đó, bây giờ chúng ta cần đưa ra một mô hình dự đoán tốt hơn. Bằng một cách nào đó, chúng ta có thể thu được mô hình như sau:
$f(x) = 0.6 \times x + 13.1$

![VD](https://tek4.vn/public_files/10f6573d-b6e4-47fc-b68e-bc3d53d96832)

Rõ ràng nhìn trên đồ thị dữ liệu, chúng ta có thể thấy mô hình này tốt hơn rất nhiều so với mô hình trước đó. Sự sai lệch giảm đi rõ rệt. Và nếu thử nhiều trường hợp hơn, chúng ta có thể thu được nhiều mô hình khác như dưới đây:

![t](https://tek4.vn/public_files/1296a06d-3669-4cc1-9db3-69ca39ce6e9a)

Và, mô hình cuối cùng cho sai số ít nhất là:
$f(x) = 0.75 \times x + 15.54$

![VD](https://tek4.vn/public_files/3abd1188-11de-4e86-a046-738b5a66c1d3)

Nhìn có khả khá là “kỳ diệu” và khó hiểu phải không ạ? Có vô số các trường hợp của tham số trong mô hinh, không lẽ chúng ta phải thử toàn bộ các tham số này (tất nhiên là không thể). Vậy chúng ta làm như thế nào? Làm sao để chúng ta có thể tính được các hệ số $m_1, m_0$ phù hợp cho mô hình như ở ví dụ trên là **0.75** và **15.54**?

**Tổng quan về hàm mất mát (Loss function)**

Ở ví dụ trên, chúng ta thấy rằng để tìm được tham số cho mô hình $f(x)$, chúng ta đều xét đến một điều kiện, đó là sai số của việc dự đoán phải thấp (và càng thấp càng tốt). Đây là cơ sở cho các thuật toán machine learning. Chẳng hạn, nếu mức độ hài lòng thực sự của nhân viên A là 60 nhưng mô hình 1 của chúng ta lại dự đoán là 40 thì sai số của việc dự đoán là 20, còn mô hình 2 dự đoán là 55 thì sai số dự đoán chỉ là 5 (và tất nhiên tốt hơn mô hình 1). Để kết quả dự đoán tốt nhất thông thường chúng ta cần tính một đại lượng gọi là lỗi dự đoán trung bình trên toàn bộ tập huấn luyện, và mục tiêu của các thuật toán machine learning là làm thế nào để lỗi dự đoán trung bình này là thấp nhất.

Đến đây, chúng ta lại bắt đầu có một vấn đề khó khăn, uh thì muốn tìm giá trị thấp nhất của lỗi trung bình nhưng mà tìm như thế nào? Chúng ta chẳng thể nào vét cạn và thử toàn bộ các giá trị của mô hình được phải không?

Để giải đáp cho vấn đề này, sức mạnh của các công cụ toán học được thể hiện. Chúng ta quay lại bài toán mà chúng ta vẫn hay làm ở cấp 3 đó là khảo sát và tìm cực trị của hàm số. Chẳng hạn chúng ta biết rằng cực trị của hàm số $x^2 + 2$ là 2 đạt tại điểm $x = 0$ thông qua các công cụ toán học (đạo hàm bằng 0). Điều này dẫn đến một điều rằng:

```
_"Nếu chúng ta có thể mô hình hóa các lỗi trung bình của việc dự đoán thành dạng một hàm số thì chúng ta hoàn toàn có thể tìm được các giá trị tham số để tối ưu hàm số đó, tức là tìm được các giá trị để cho hàm số đạt giá trị nhỏ nhất, hay lỗi dự đoán là nhỏ nhất trên tập huấn luyện. Kết quả này chính là mô hình chúng ta cần xây dựng và quá trình để tìm nghiệm này được gọi là quá trình huấn luyện mô hình."_
```

Các hàm số đại diện cho lỗi dự đoán trung bình này được gọi là các hàm mất mát (loss function hay còn gọi là hàm phạt), thể hiện mức độ dự đoán sai của mô hình so với dữ liệu huấn luyện. Nó thường được suy ra từ độ đo P và bổ sung thêm một số suy luận, biến đổi để hàm số này trở lên dễ tối ưu (tức là hàm trơn, có đạo hàm, lồi và có nghiệm tối ưu càng dễ tìm càng tốt).

Với nguyên tắc này, quay lại ví dụ trên ta có thể xây dựng một hàm mất mát (loss function) có dạng là hàm bình phương (linear least squares function):

[Đọc tiếp](https://tek4.vn/khoa-hoc/machine-learning-co-ban/luong-cang-cao-se-cang-hanh-phuc-vi-du-dau-tien-ve-machine-learning)
