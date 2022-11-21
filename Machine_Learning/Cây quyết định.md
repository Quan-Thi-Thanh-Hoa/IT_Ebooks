# Hướng dẫn đầy đủ về cây quyết định

Ban đầu, học máy học máy (ML) có thể đáng sợ. Các thuật ngữ như “Gradient Descent”("giảm dần độ dốc"), “Latent Dirichlet Allocation”("phân bổ Dirichlet tiềm ẩn") hoặc “Convolutional Layer”("lớp chập") có thể khiến nhiều người sợ hãi. Nhưng có những cách thân thiện để đi vào kỷ luật, và tôi nghĩ bắt đầu với những cây quyết định là một quyết định khôn ngoan.

Cây quyết định (DTS) có lẽ là một trong những thuật toán học tập được giám sát hữu ích nhất hiện có. Trái ngược với việc học không được giám sát (trong đó không có biến đầu ra để hướng dẫn quá trình học tập và dữ liệu được khám phá bởi các thuật toán để tìm các mẫu), trong việc học dữ liệu hiện tại của bạn đã được dán nhãn và bạn biết bạn muốn dự đoán hành vi nào trong dữ liệu mới Bạn được thông qua. Đây là loại thuật toán mà ô tô tự trị sử dụng để nhận ra người đi bộ và đối tượng, hoặc các tổ chức khai thác để ước tính giá trị trọn đời của khách hàng và tỷ lệ khu vực của họ.

> Theo một cách nào đó, việc học có giám sát giống như học với một giáo viên, và sau đó áp dụng kiến ​​thức đó vào dữ liệu mới.

DTS là các thuật toán ML phân chia các tập dữ liệu dần dần thành các nhóm dữ liệu nhỏ hơn dựa trên tính năng mô tả, cho đến khi chúng đạt được các bộ đủ nhỏ để được mô tả bởi một số nhãn. Họ yêu cầu bạn có dữ liệu được dán nhãn (được gắn thẻ với một hoặc nhiều nhãn, như tên thực vật trong hình ảnh của thực vật), vì vậy họ cố gắng gắn nhãn dữ liệu mới dựa trên kiến ​​thức đó.

Các thuật toán DTS là hoàn hảo để giải quyết phân loại (trong đó máy sắp xếp dữ liệu thành các lớp, như liệu email có phải là spam hay không) và hồi quy (trong đó máy dự đoán các giá trị, như giá tài sản). Cây hồi quy được sử dụng khi biến phụ thuộc là liên tục hoặc định lượng (ví dụ: nếu chúng tôi muốn ước tính xác suất khách hàng sẽ mặc định cho khoản vay) và các cây phân loại được sử dụng khi biến phụ thuộc là phân loại hoặc định tính (ví dụ: nếu chúng tôi muốn Ước tính loại máu của một người).

Tầm quan trọng của DTS dựa trên thực tế là họ có rất nhiều ứng dụng trong thế giới thực. Là một trong những thuật toán được sử dụng chủ yếu trong ML, chúng được áp dụng cho các chức năng khác nhau trong một số ngành:

- DTS đang được sử dụng trong ngành chăm sóc sức khỏe để cải thiện việc sàng lọc các trường hợp tích cực trong việc phát hiện sớm suy giảm nhận thức, và cũng để xác định các yếu tố rủi ro chính của việc phát triển một số loại chứng mất trí nhớ trong tương lai.
- Sophia, robot được làm công dân Ả Rập Saudi, sử dụng các thuật toán DTS để trò chuyện với con người. Trên thực tế, chatbot sử dụng các thuật toán này đã mang lại lợi ích trong các ngành công nghiệp như bảo hiểm y tế bằng cách thu thập dữ liệu từ khách hàng thông qua việc áp dụng các cuộc khảo sát sáng tạo và trò chuyện thân thiện. Google gần đây đã mua lại Onward, một công ty sử dụng DTS để phát triển các chatbot có chức năng đặc biệt trong việc cung cấp dịch vụ chăm sóc khách hàng đẳng cấp thế giới và Amazon đang đầu tư theo cùng một hướng để hướng dẫn khách hàng nhanh chóng đến con đường giải quyết.
- Có thể dự đoán các nguyên nhân có khả năng gây rối loạn rừng, như cháy rừng, khai thác các đồn điền cây, nông nghiệp quy mô lớn hoặc nhỏ và đô thị hóa bằng cách đào tạo DTS để nhận ra các nguyên nhân khác nhau của mất rừng từ hình ảnh vệ tinh. DTS và hình ảnh vệ tinh cũng được sử dụng trong nông nghiệp để phân loại các loại cây trồng khác nhau và xác định các giai đoạn hiện tượng của chúng.
- DTS là những công cụ tuyệt vời để thực hiện phân tích tình cảm của các văn bản và xác định cảm xúc đằng sau chúng. Phân tích tình cảm là một kỹ thuật mạnh mẽ có thể giúp các tổ chức tìm hiểu về lựa chọn của khách hàng và trình điều khiển quyết định của họ.
- Trong khoa học môi trường, DTS có thể giúp xác định chiến lược tốt nhất để đối phó với các loài xâm lấn, từ loại trừ đến ngăn chặn và giảm thiểu lây lan.
- DTS cũng được sử dụng để cải thiện phát hiện gian lận tài chính. MIT cho thấy rằng nó có thể cải thiện đáng kể hiệu suất của các mô hình ML thay thế bằng cách sử dụng DT được đào tạo với một số nguồn dữ liệu thô để tìm các mẫu giao dịch và thẻ tín dụng phù hợp với các trường hợp gian lận.

DTS cực kỳ phổ biến vì nhiều lý do, là khả năng diễn giải của họ có lẽ là lợi thế quan trọng nhất của họ. Chúng có thể được đào tạo rất nhanh và dễ hiểu, điều này mở ra khả năng của chúng đối với các biên giới vượt xa các bức tường khoa học. Ngày nay, DTS rất phổ biến trong môi trường kinh doanh và việc sử dụng của họ cũng đang mở rộng đến các khu vực dân sự, nơi một số ứng dụng đang làm tăng mối quan tâm lớn.

Công ty Sesame Credit (một công ty liên kết với Alibaba) sử dụng DTS và các thuật toán khác để động cơ một hệ thống đánh giá xã hội, xem xét các yếu tố khác nhau như đúng giờ mà các hóa đơn được thanh toán và các hoạt động trực tuyến khác. Lợi ích của một "điểm mè" tốt ở Trung Quốc bao gồm từ khả năng hiển thị cao hơn trên các trang web hẹn hò đến bỏ qua đường chờ nếu bạn cần gặp bác sĩ. Trên thực tế, sau khi chính phủ Trung Quốc tuyên bố sẽ áp dụng cái gọi là hệ thống tín dụng xã hội của mình cho các chuyến bay và tàu hỏa và ngăn chặn những người đã thực hiện hành vi sai trái khi thực hiện vận chuyển như vậy trong một năm, có một mối lo ngại rằng hệ thống cuối cùng sẽ tạo ra một "Big Brother được hỗ trợ bởi ML".

## Những thứ cơ bản

Trong bộ phim Bandersnatch (một tập phim Black Mirror độc lập từ Netflix), người xem có thể tương tác chọn các đường dẫn kể chuyện khác nhau và đạt được các câu chuyện và kết thúc khác nhau. Có một loạt các quyết định phức tạp ẩn đằng sau cách kể chuyện phim cho phép khán giả di chuyển trong một loại chọn chế độ phiêu lưu của riêng bạn, mà Netflix phải tìm ra cách tải nhiều phiên bản của mỗi cảnh trong khi trình bày nó một cách đơn giản . Trong thực tế, những gì các nhà sản xuất Netflix đã làm là phân đoạn bộ phim và đặt các điểm chi nhánh khác nhau để người xem di chuyển qua và đưa ra kết quả khác nhau. Nói cách khác, điều này giống như xây dựng một DT.

DT bao gồm các nút, cành và lá. Mỗi nút đại diện cho một thuộc tính (hoặc tính năng), mỗi nhánh đại diện cho một quy tắc (hoặc quyết định) và mỗi lá đại diện cho một kết quả. Độ sâu của một cây được xác định bởi số lượng cấp độ, không bao gồm nút gốc.

![A](https://miro.medium.com/max/828/0*IS9xKHt83nuERC9P)

DTS áp dụng cách tiếp cận từ trên xuống cho dữ liệu, do đó, đã đưa ra một tập dữ liệu, họ cố gắng nhóm và các quan sát nhãn tương tự giữa chúng và tìm kiếm các quy tắc tốt nhất phân chia các quan sát không giống nhau giữa chúng cho đến khi chúng đạt đến mức độ nhất định của sự tương đồng.

> _Họ sử dụng một quy trình phân tách lớp, trong đó mỗi lớp họ cố gắng chia dữ liệu thành hai hoặc nhiều nhóm, do đó dữ liệu rơi vào cùng một nhóm giống nhau (tính đồng nhất) và các nhóm khác nhau nhất có thể so với nhau (không đồng nhất)._

Việc phân tách có thể là nhị phân (chia mỗi nút thành tối đa hai nhóm phụ và cố gắng tìm phân vùng tối ưu) hoặc nhiều đường (chia mỗi nút thành nhiều nhóm phụ, sử dụng nhiều phân vùng như các giá trị khác biệt hiện có). Trong thực tế, thông thường là thấy DTS với sự phân chia nhị phân, nhưng điều quan trọng là phải biết rằng việc chia tách nhiều đường có một số lợi thế. Multiway chia tách tất cả thông tin trong một thuộc tính danh nghĩa, điều đó có nghĩa là một thuộc tính hiếm khi xuất hiện nhiều hơn một lần trong bất kỳ đường dẫn từ gốc đến lá, giúp DT dễ hiểu hơn. Trên thực tế, cách tốt nhất để phân chia dữ liệu có thể là tìm một tập hợp các khoảng thời gian cho một tính năng nhất định, sau đó chia dữ liệu đó thành nhiều nhóm dựa trên các khoảng thời gian đó.

![A](https://miro.medium.com/max/828/0*EhzZNP_6Y7jdJgO9)

Theo thuật ngữ hai chiều (chỉ sử dụng 2 biến), DTS phân vùng vũ trụ dữ liệu thành một tập hợp các hình chữ nhật và phù hợp với một mô hình trong mỗi một hình chữ nhật đó. Chúng đơn giản nhưng mạnh mẽ, và là một công cụ tuyệt vời cho các nhà khoa học dữ liệu.

![B](https://miro.medium.com/max/828/0*cant-HQdfMju-GxG)

**Hình bên phải cho thấy phân vùng của không gian dữ liệu hai chiều do DT tạo ra ở bên trái (phân chia nhị phân). Tuy nhiên, trong thực tế, DTS sử dụng nhiều biến (thường là hơn 2).**

Mỗi nút trong DT hoạt động như một trường hợp thử nghiệm cho một số điều kiện và mỗi nhánh giảm dần từ nút đó tương ứng với một trong các câu trả lời có thể cho trường hợp thử nghiệm đó.

## Prune that Tree

Khi số lượng phân tách trong DTS tăng, độ phức tạp của chúng tăng lên. Nói chung, các DT đơn giản hơn được ưu tiên hơn những người siêu phức tạp, vì chúng dễ hiểu hơn và chúng ít bị rơi vào quá mức.

**Việc đặt quá mức đề cập đến một mô hình tìm hiểu dữ liệu đào tạo (dữ liệu mà nó sử dụng để tìm hiểu) tốt đến mức nó có vấn đề để khái quát hóa dữ liệu mới (chưa nhìn thấy).**

Nói cách khác, mô hình tìm hiểu chi tiết và tiếng ồn (thông tin không liên quan hoặc tính ngẫu nhiên trong bộ dữ liệu) trong dữ liệu đào tạo đến mức nó tác động tiêu cực đến hiệu suất của mô hình trên dữ liệu mới. Điều này có nghĩa là tiếng ồn hoặc biến động ngẫu nhiên trong dữ liệu đào tạo được chọn và học dưới dạng các khái niệm của mô hình.

![a](https://miro.medium.com/max/640/1*c3W5mjgvBRIOFA8ye1JEXg.png)

**Trong khi dòng màu đen phù hợp với dữ liệu tốt, đường màu xanh lá cây đang quá mức**

Trong điều kiện này, mô hình của bạn hoạt động hoàn toàn tốt với dữ liệu bạn cung cấp trả trước, nhưng khi bạn hiển thị cùng một mô hình đó với dữ liệu mới, nó sẽ bị hỏng. Nó không thể lặp lại hiệu suất rất chi tiết của nó.

Vì vậy, làm thế nào để bạn tránh quá mức trong DTS? Bạn cần loại trừ các nhánh phù hợp với dữ liệu quá cụ thể. Bạn muốn một DT có thể khái quát và hoạt động tốt trên dữ liệu mới, mặc dù điều này có thể ngụ ý mất độ chính xác trên dữ liệu đào tạo. Luôn luôn tốt hơn để tránh một mô hình DT tìm hiểu và lặp lại các chi tiết cụ thể như một con vẹt và cố gắng phát triển một mô hình có sức mạnh và tính linh hoạt để có hiệu suất tốt trên dữ liệu mới mà bạn cung cấp cho nó.

> _Cắt tỉa là một kỹ thuật được sử dụng để đối phó với quá mức, làm giảm kích thước của DT bằng cách loại bỏ các phần của cây cung cấp ít sức mạnh dự đoán hoặc phân loại._

Mục tiêu của thủ tục này là giảm độ phức tạp và đạt được độ chính xác tốt hơn bằng cách giảm tác động của việc quá mức và loại bỏ các phần của DT có thể dựa trên dữ liệu ồn ào hoặc sai lầm. Có hai chiến lược khác nhau để thực hiện việc cắt tỉa trên DTS:

- Tiền tôi: Khi bạn ngừng phát triển các nhánh DT khi thông tin trở nên không đáng tin cậy.
- Post-Prune: Khi bạn thực hiện một DT phát triển hoàn toàn và sau đó loại bỏ các nút lá chỉ khi nó dẫn đến hiệu suất mô hình tốt hơn. Bằng cách này, bạn ngừng loại bỏ các nút khi không có cải thiện nào nữa.

![A](https://miro.medium.com/max/828/0*ubL8_k7w3JNEvZ18)

**Ví dụ về một DT không được kiểm soát, như được lấy từ DataCamp**

## Thuật toán DTS chính

Bây giờ bạn có thể tự hỏi: Làm thế nào để DTS biết các tính năng nào sẽ chọn và làm thế nào để phân chia dữ liệu? Để hiểu điều đó, chúng ta cần phải có được một số chi tiết.

> _Tất cả các DT thực hiện về cơ bản cùng một nhiệm vụ: họ kiểm tra tất cả các thuộc tính của tập dữ liệu để tìm các thuộc tính cho kết quả tốt nhất có thể bằng cách chia dữ liệu thành các nhóm con. Họ thực hiện nhiệm vụ này một cách đệ quy bằng cách chia các nhóm con thành các đơn vị nhỏ hơn và nhỏ hơn cho đến khi cây kết thúc (dừng lại bởi một số tiêu chí nhất định)._

[The Complete Guide to Decision Trees](https://towardsdatascience.com/the-complete-guide-to-decision-trees-28a4e3c7be14)
