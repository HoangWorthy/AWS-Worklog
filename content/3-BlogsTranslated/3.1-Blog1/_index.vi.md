---
title: "Blog 1"
date: 
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Tăng tốc quy trình xử lý yêu cầu quyền lợi với Amazon Bedrock Data Automation

Trong ngành quản lý quyền lợi nhân sự (benefits administration), xử lý yêu cầu quyền lợi (claims processing) là một trụ cột vận hành quan trọng, đảm bảo rằng nhân viên và người thụ hưởng nhận được quyền lợi đúng hạn — chẳng hạn như thanh toán bảo hiểm y tế, nha khoa hoặc tàn tật — đồng thời kiểm soát chi phí và tuân thủ các quy định như HIPAA và ERISA. Các doanh nghiệp hướng đến việc tối ưu hóa quy trình làm việc — bao gồm nộp yêu cầu, xác minh, thẩm định, thanh toán và khiếu nại — nhằm nâng cao sự hài lòng của nhân viên, củng cố mối quan hệ với nhà cung cấp dịch vụ, và giảm thiểu rủi ro tài chính. Quy trình này bao gồm các bước cụ thể như nộp yêu cầu (thông qua cổng trực tuyến hoặc biểu mẫu giấy), xác minh dữ liệu (kiểm tra tính hợp lệ và chính xác), thẩm định (đánh giá phạm vi quyền lợi dựa trên quy tắc của gói bảo hiểm), thanh toán hoặc từ chối (bao gồm xử lý chi phiếu hoàn tiền), và xử lý khiếu nại. Một quy trình xử lý hiệu quả hỗ trợ cung cấp các chương trình phúc lợi cạnh tranh — yếu tố quan trọng để thu hút và giữ chân nhân tài, cũng như củng cố thương hiệu nhà tuyển dụng — nhưng đồng thời yêu cầu cân bằng giữa tốc độ, độ chính xác và chi phí trong một môi trường được quản lý nghiêm ngặt.

Mặc dù có tầm quan trọng lớn, quy trình xử lý yêu cầu vẫn gặp nhiều thách thức trong nhiều tổ chức. Đáng chú ý nhất là sự phụ thuộc vào hệ thống kế thừa (legacy systems) và quy trình thủ công (manual processes) dẫn đến thời gian xử lý chậm, tỷ lệ lỗi cao và chi phí hành chính tăng. Các yêu cầu không đầy đủ hoặc sai sót — chẳng hạn như thiếu mã chẩn đoán hoặc không khớp điều kiện hưởng — thường dẫn đến việc từ chối và xử lý lại, gây ra sự khó chịu cho cả nhân viên lẫn nhà cung cấp dịch vụ y tế. Bên cạnh đó, gian lận, lãng phí và lạm dụng (fraud, waste, and abuse) tiếp tục làm tăng chi phí, trong khi việc phát hiện những vấn đề này mà không trì hoãn các yêu cầu hợp lệ vẫn là một thách thức. Các yêu cầu pháp lý phức tạp đòi hỏi hệ thống phải được cập nhật liên tục, và việc tích hợp kém giữa các hệ thống — chẳng hạn giữa Human Resource Information Systems (HRIS) và các hệ thống xử lý kế tiếp — hạn chế nghiêm trọng khả năng mở rộng. Những vấn đề này làm tăng chi phí vận hành, xói mòn niềm tin vào chương trình phúc lợi, và khiến các nhóm hỗ trợ khách hàng bị quá tải, đặc biệt trong các giai đoạn xử lý khiếu nại hoặc cao điểm yêu cầu quyền lợi.

Generative AI có thể giúp giải quyết những thách thức này. Với Amazon Bedrock Data Automation, bạn có thể tự động hóa việc tạo ra các insight hữu ích từ nội dung phi cấu trúc đa phương tiện như tài liệu, hình ảnh, âm thanh và video. Amazon Bedrock Data Automation có thể được sử dụng trong quy trình xử lý yêu cầu quyền lợi để tự động hóa việc xử lý tài liệu bằng cách trích xuất và phân loại tài liệu từ các gói yêu cầu, đơn đăng ký chính sách và tài liệu hỗ trợ với độ chính xác hàng đầu trong ngành, giúp giảm thiểu lỗi thủ công và tăng tốc thời gian xử lý. Khả năng xử lý ngôn ngữ tự nhiên (Natural Language Processing - NLP) của Amazon Bedrock Data Automation cho phép hiểu và diễn giải dữ liệu phi cấu trúc như ghi chú của nhà cung cấp, hỗ trợ tuân thủ các quy tắc và quy định của chương trình phúc lợi. Bằng cách tự động hóa các nhiệm vụ lặp lại và cung cấp insight, Amazon Bedrock Data Automation giúp giảm gánh nặng hành chính, cải thiện trải nghiệm của cả nhân viên và nhà cung cấp, đồng thời hỗ trợ tuân thủ quy định với chi phí hiệu quả. Hơn nữa, kiến trúc có khả năng mở rộng (scalable architecture) của nó cho phép tích hợp liền mạch với các hệ thống hiện có, cải thiện luồng dữ liệu giữa HRIS, hệ thống xử lý yêu cầu và mạng lưới nhà cung cấp. Các phân tích nâng cao (advanced analytics) cũng giúp phát hiện các mô hình gian lận để tối ưu hóa kiểm soát chi phí.

Trong bài viết này, chúng ta sẽ xem xét quy trình xử lý yêu cầu quyền lợi điển hình và xác định nơi mà tự động hóa được hỗ trợ bởi Generative AI có thể mang lại tác động lớn nhất.

---

## Xử lý yêu cầu bồi hoàn quyền lợi

Khi một nhân viên hoặc người thụ hưởng tự chi trả cho một khoản chi phí nằm trong phạm vi quyền lợi bảo hiểm y tế của họ, họ sẽ gửi yêu cầu bồi hoàn (claim) để được hoàn tiền. Quy trình này yêu cầu nhiều tài liệu hỗ trợ, bao gồm đơn thuốc của bác sĩ và bằng chứng thanh toán — có thể là hình ảnh séc, biên lai hoặc xác nhận thanh toán điện tử.
Quy trình xử lý yêu cầu bồi hoàn bao gồm một số bước quan trọng sau:

* Tiếp nhận và xử lý tài liệu – Hệ thống nhận và phân loại các tài liệu được gửi, bao gồm:
  * Hồ sơ y tế và đơn thuốc
  * Tài liệu chứng minh thanh toán
  * Các biểu mẫu hỗ trợ và xác minh quyền đủ điều kiện
* Xử lý xác minh thanh toán – Đối với các khoản bồi hoàn dựa trên séc, hệ thống cần thực hiện các bước sau:
  * Trích xuất thông tin từ hình ảnh séc, bao gồm số tài khoản và số định tuyến (routing number) trong dòng MICR
  * Xác minh tên người nhận và người chi trả dựa trên thông tin được cung cấp trong quá trình gửi yêu cầu
  * Xác nhận rằng số tiền thanh toán khớp với chi phí được yêu cầu bồi hoàn
  * Đánh dấu các sai lệch để chuyển cho nhân viên kiểm tra thủ công
* Thẩm định và hoàn tiền – Khi quá trình xác minh hoàn tất, hệ thống thực hiện các hành động sau:
  * Xác định quyền lợi dựa trên quy định của gói bảo hiểm và giới hạn chi trả
  * Tính toán số tiền hoàn trả phù hợp
  * Khởi tạo quy trình thanh toán thông qua chuyển khoản trực tiếp hoặc phát hành séc
  * Gửi thông báo đến người yêu cầu về trạng thái hoàn tiền của họ

Trong bài viết này, chúng tôi sẽ trình bày một ví dụ thực tế để giúp làm rõ tính phức tạp của quy trình nhiều bước này. Ví dụ sau minh họa cách Amazon Bedrock Data Automation có thể tối ưu hóa quy trình xử lý yêu cầu bồi hoàn, từ bước gửi ban đầu đến khi hoàn tất chi trả.


## Tổng quan giải pháp

Giả sử một người tham gia chương trình quyền lợi bảo hiểm đến khám bác sĩ và tự chi trả bằng séc. Sau đó, họ mua thuốc được bác sĩ kê tại nhà thuốc. Sau cùng, họ đăng nhập vào cổng thông tin của nhà cung cấp quyền lợi và gửi yêu cầu bồi hoàn kèm hình ảnh séc và biên lai thanh toán tiền thuốc.
Giải pháp này sử dụng Amazon Bedrock Data Automation để tự động hóa hai khía cạnh quan trọng và tốn thời gian nhất trong quy trình: tiếp nhận tài liệu và xác minh thanh toán. Sơ đồ sau minh họa kiến trúc xử lý yêu cầu bồi hoàn quyền lợi.

![System Architecture](/images/blog-1-1.png)
Quy trình tổng thể hoạt động qua bốn giai đoạn tích hợp: nhập dữ liệu, trích xuất dữ liệu, kiểm tra, và tích hợp.
### Nhập dữ liệu

Khi người thụ hưởng tải lên các tài liệu hỗ trợ (hình ảnh séc và biên lai nhà thuốc) thông qua cổng thông tin yêu cầu bồi hoàn của công ty, các tài liệu này sẽ được lưu trữ an toàn trong một Amazon Simple Storage Service (Amazon S3) bucket, kích hoạt pipeline tự động xử lý yêu cầu hoàn tiền.

### Trích xuất dữ liệu

Sau khi các tài liệu được tải lên, hệ thống ngay lập tức bắt đầu quá trình trích xuất dữ liệu thông minh:
Tải đối tượng S3 (S3 object upload) kích hoạt một AWS Lambda function, hàm này sẽ gọi Amazon Bedrock Data Automation project.
Amazon Bedrock Data Automation sử dụng các blueprints để xử lý và trích xuất dữ liệu từ tệp. Blueprints là các cấu phần (artifact) được dùng để cấu hình logic nghiệp vụ xử lý tệp bằng cách chỉ định danh sách các trường dữ liệu cần trích xuất, định dạng dữ liệu mong muốn (string, number hoặc Boolean), cùng ngữ cảnh ngôn ngữ tự nhiên phục vụ chuẩn hóa dữ liệu và thiết lập quy tắc xác thực. Amazon Bedrock Data Automation cung cấp sẵn một danh mục các blueprint mẫu. Bạn có thể tạo blueprint tùy chỉnh cho các loại tài liệu đặc thù không có trong danh mục mặc định. Trong giải pháp này, hai blueprint được sử dụng tương ứng cho các loại tài liệu khác nhau, như minh họa trong hình dưới:

* US-Bank-Check: blueprint có sẵn trong danh mục để xử lý séc ngân hàng.
* benefit-claims-pharmacy-receipt-blueprint: blueprint tùy chỉnh dành cho biên lai nhà thuốc.

![System Architecture](/images/blog-1-2.png)

US-Bank-Check là một blueprint tiêu chuẩn được cung cấp sẵn bởi Amazon Bedrock Data Automation. Trong khi đó, blueprint tùy chỉnh benefit-claims-pharmacy-receipt-blueprint được tạo thông qua AWS CloudFormation template để xử lý biên lai nhà thuốc — một loại tài liệu chưa được hỗ trợ trong danh mục blueprint mặc định. Quản trị viên quyền lợi (benefit administrator) muốn trích xuất thông tin liên quan đến nhà cung cấp (vendor) như tên, địa chỉ và số điện thoại trong quá trình xử lý yêu cầu bồi hoàn. Blueprint tùy chỉnh này định nghĩa schema chứa mô tả ngôn ngữ tự nhiên cho các trường dữ liệu như VendorName, VendorAddress, VendorPhone, và các trường bổ sung khác — nêu rõ ý nghĩa, kiểu dữ liệu mong đợi, và loại suy luận (inference type) của từng trường trích xuất (như được mô tả trong phần Creating Blueprints for Extraction), được minh họa trong hình dưới:

![System Architecture](/images/blog-1-3.png)

Hai blueprint này được thêm vào Amazon Bedrock Data Automation project. Một project trong Amazon Bedrock Data Automation là tập hợp các blueprint chuẩn và tùy chỉnh, cho phép xử lý nhiều loại tệp khác nhau (ví dụ: tài liệu, âm thanh, hình ảnh) với cấu hình riêng biệt. Bạn có thể kiểm soát loại thông tin cần trích xuất từ từng loại tệp. Khi project được kích hoạt bất đồng bộ (asynchronously invoked), hệ thống sẽ tự động áp dụng blueprint phù hợp, trích xuất các thông tin như confidence scores và bounding box details cho từng trường dữ liệu, rồi lưu kết quả vào một S3 bucket riêng biệt. Cơ chế phân loại thông minh này giúp loại bỏ nhu cầu viết thủ công các thuật toán phân loại tài liệu phức tạp.

Hình dưới đây minh họa quá trình phân loại tài liệu bởi blueprint tiêu chuẩn US-Bank-Check:

![System Architecture](/images/blog-1-4.jpg)

Hình tiếp theo thể hiện kết quả phân loại tài liệu sử dụng blueprint tùy chỉnh 

benefit-claims-pharmacy-receipt-blueprint:


![System Architecture](/images/blog-1-5.png)

Sau khi dữ liệu được trích xuất, hệ thống chuyển sang giai đoạn xác thực và ra quyết định, dựa trên các quy tắc nghiệp vụ (business rules) được định nghĩa riêng cho từng loại tài liệu.

Các quy tắc nghiệp vụ này được mô tả trong các tài liệu quy trình vận hành tiêu chuẩn (AnyCompany Benefit Checks Standard Operating procedure.docx và AnyCompany Benefit Claims Standard Operating procedure.docx) và được tải lên Amazon S3 bucket. Sau đó hệ thống tạo knowledge base cho Amazon Bedrock, sử dụng bucket này làm nguồn dữ liệu, như minh họa trong hình bên dưới:

![System Architecture](/images/blog-1-6.jpg)

Khi kết quả trích xuất từ Amazon Bedrock Data Automation được lưu trong S3 bucket đã cấu hình, một AWS Lambda function sẽ được tự động kích hoạt. Dựa trên các quy tắc nghiệp vụ lấy từ knowledge base tương ứng với từng loại tài liệu và dữ liệu đầu ra từ Amazon Bedrock Data Automation, mô hình ngôn ngữ lớn Amazon Nova Lite sẽ thực hiện tự động phê duyệt hoặc từ chối (approve/deny) các yêu cầu hoàn tiền.

Hình dưới đây minh họa kết quả tự động phê duyệt yêu cầu bồi hoàn cho blueprint US-Bank-Check:


![System Architecture](/images/blog-1-7.png)

Hình tiếp theo minh họa kết quả tự động phê duyệt cho blueprint benefit-claims-pharmacy-receipt-blueprint:

![System Architecture](/images/blog-1-8.png)

### Tích hợp

Hệ thống được thiết kế để tích hợp liền mạch với quy trình nghiệp vụ hiện có.

Khi quá trình xác thực hoàn tất, một sự kiện (event) sẽ được gửi đến Amazon EventBridge, kích hoạt Lambda function để xử lý tích hợp downstream. Trong triển khai này, hệ thống sử dụng Amazon DynamoDB và Amazon Simple Notification Service (Amazon SNS) để phục vụ việc tích hợp. Một bảng DynamoDB được tạo như một phần của deployment stack, dùng để lưu thông tin như phân loại tài liệu, dữ liệu trích xuất, và quyết định tự động. Thông báo email được gửi thông qua Amazon SNS cho cả trường hợp séc và biên lai sau khi hệ thống đưa ra quyết định cuối cùng.

Hình dưới minh họa ví dụ email thông báo phê duyệt cho biên lai nhà thuốc:

![System Architecture](/images/blog-1-9.jpeg)

Kiến trúc linh hoạt này cho phép bạn tích hợp với các ứng dụng nội bộ thông qua API hoặc sự kiện (event) để cập nhật trạng thái yêu cầu hoàn tiề hoặc kích hoạt quy trình bổ sung khi việc xác thực không thành công.
## Giảm thiểu nỗ lực thủ công bằng quản lý quy tắc nghiệp vụ thông minh

Bên cạnh việc tự động hóa xử lý tài liệu, giải pháp này còn giải quyết một thách thức vận hành phổ biến: Trước đây, khách hàng phải tự viết và duy trì mã nguồn (code) để xử lý các quy tắc nghiệp vụ (business rules) liên quan đến xét duyệt (adjudication) và xử lý yêu cầu bồi hoàn (claims processing). Mỗi khi có sự thay đổi về quy tắc nghiệp vụ, nhóm phát triển phải cập nhật mã, dẫn đến tăng thời gian triển khai, giảm tốc độ đưa sản phẩm ra thị trường (time-to-market), và gia tăng chi phí bảo trì. 

Cách tiếp cận mới sử dụng Amazon Bedrock Knowledge Bases để chuyển đổi các quy tắc nghiệp vụ và tài liệu quy trình vận hành tiêu chuẩn (Standard Operating Procedures - SOPs) thành cơ sở tri thức (knowledge bases) phục vụ tự động ra quyết định (automated decision-making). Cách tiếp cận này có thể rút ngắn đáng kể thời gian triển khai khi có thay đổi về quy tắc nghiệp vụ, vì các cập nhật có thể được thực hiện thông qua quản lý tri thức thay vì triển khai lại mã nguồn.

Trong các phần tiếp theo, chúng tôi sẽ hướng dẫn bạn từng bước triển khai giải pháp vào tài khoản AWS của riêng bạn.


---

## Yêu cầu ban đầu

Để triển khai giải pháp được trình bày trong bài viết này, bạn cần:
* Một tài khoản AWS account
* Quyền truy cập Amazon Titan Text Embeddings V2 và Amazon Nova Lite foundation models (FMs) đã được kích hoạt trong Amazon Bedrock
* 
Giải pháp này sử dụng Python 3.13 với Boto3 phiên bản 1.38 hoặc cao hơn, cùng AWS Serverless Application Model Command Line Interface (AWS SAM CLI) phiên bản 1.138.0. Chúng tôi giả định bạn đã cài đặt các công cụ này trên máy cục bộ. Nếu chưa, hãy tham khảo các hướng dẫn sau:

* Python 3.13 installation
* Install the AWS SAM CLI

---

## Thiết lập mã nguồn trong máy cục bộ

Để thiết lập mã, clone GitHub repository chứa mã nguồn của giải pháp.

Sau khi clone về máy, cấu trúc thư mục dự án sẽ giống như ví dụ trong tệp README:

![System Architecture](/images/blog-1-10.png)

## Triển khai giải pháp trong tài khoản của bạn

Mã mẫu đi kèm với CloudFormation template, giúp tự động tạo các tài nguyên cần thiết.Để triển khai giải pháp trên tài khoản AWS của bạn, hãy làm theo hướng dẫn triển khai trong README file.

## Dọn dẹp

Việc triển khai giải pháp này trong tài khoản AWS sẽ phát sinh chi phí sử dụng dịch vụ. Hãy làm theo hướng dẫn dọn dẹp trong README file để tránh bị tính phí sau khi bạn đã hoàn tất thử nghiệm.

## Kết luận

Các công ty trong lĩnh vực quản lý quyền lợi nhân viên (benefits administration) có thể nâng cao đáng kể hiệu quả vận hành bằng cách tự động hóa xử lý yêu cầu bồi hoàn (claims processing) thông qua giải pháp được trình bày trong bài viết này. Cách tiếp cận chiến lược này trực tiếp giải quyết các thách thức cốt lõi của ngành, mang lại nhiều lợi ích then chốt:

Nâng cao hiệu suất xử lý nhờ tăng tốc thời gian giải quyết yêu cầu, giảm lỗi thủ công, và tăng tỷ lệ xử lý tự động (straight-through processing rate), giúp loại bỏ tình trạng chậm trễ và khối lượng tái xử lý lớn từ các hệ thống cũ.
Hợp nhất xử lý tài liệu và phát hiện gian lận nhờ các blueprint mới trong Amazon Bedrock Data Automation, cho phép tích hợp nhanh các loại tài liệu hỗ trợ mới, đồng thời AI-powered analytics phát hiện mẫu gian lận (fraud patterns) mà không làm chậm yêu cầu hợp lệ, giảm thiểu chi phí gian lận, lãng phí và sai phạm.

Quản lý quy tắc nghiệp vụ linh hoạt (Agile business rule management) cho phép thích ứng nhanh với các yêu cầu thay đổi của HIPAA và ERISA, giúp giảm chi phí vận hành, rút ngắn thời gian triển khai, tăng khả năng mở rộng và tích hợp với các hệ thống HRIS và claims hiện có. Điều này giúp nâng cao sự hài lòng của nhân viên, củng cố mối quan hệ với nhà cung cấp dịch vụ, và duy trì sức cạnh tranh trong chính sách phúc lợi, yếu tố quan trọng trong giữ chân nhân tài và xây dựng thương hiệu nhà tuyển dụng (employer branding).

Để bắt đầu với giải pháp này, hãy tham khảo GitHub repo được cung cấp. Để tìm hiểu thêm về Amazon Bedrock Data Automation, vui lòng xem bài viết “Transform unstructured data into meaningful insights using Amazon Bedrock Data Automation” và tham gia workshop “Document Processing Using Amazon Bedrock Data Automation”.
