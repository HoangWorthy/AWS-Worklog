---
title: "Blog 3"
date: 
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---



# Cách PropHero xây dựng một cố vấn đầu tư bất động sản thông minh với khả năng đánh giá liên tục bằng Amazon Bedrock

PropHero là một dịch vụ quản lý tài sản bất động sản hàng đầu, giúp dân chủ hóa khả năng tiếp cận các lời khuyên đầu tư bất động sản thông minh thông qua big data, AI và machine learning (ML). Đối với cơ sở khách hàng tại Tây Ban Nha và Úc, PropHero cần một hệ thống tư vấn được hỗ trợ bởi AI có khả năng tương tác với khách hàng trong các cuộc thảo luận đầu tư bất động sản một cách chính xác. Mục tiêu là cung cấp các phân tích đầu tư cá nhân hóa và hướng dẫn, hỗ trợ người dùng ở mọi giai đoạn hành trình đầu tư: từ việc hiểu quy trình, nắm rõ mốc thời gian, tải lên tài liệu một cách an toàn, đến theo dõi tiến độ theo thời gian thực.

PropHero đã hợp tác với AWS Generative AI Innovation Center để triển khai một cố vấn đầu tư bất động sản thông minh sử dụng AWS generative AI services cùng với hệ thống đánh giá liên tục. Giải pháp cho phép người dùng tham gia các cuộc hội thoại bằng ngôn ngữ tự nhiên về các chiến lược đầu tư bất động sản và nhận các khuyến nghị cá nhân hóa dựa trên kiến thức thị trường toàn diện của PropHero.

Trong bài viết này, chúng tôi trình bày cách xây dựng một hệ thống AI hội thoại đa tác nhân (multi-agent conversational AI system) sử dụng Amazon Bedrock nhằm cung cấp lời khuyên đầu tư bất động sản được grounding trên kiến thức (knowledge-grounded). Chúng tôi sẽ phân tích kiến trúc của các agent, chiến lược lựa chọn mô hình, và hệ thống đánh giá liên tục toàn diện — những thành phần giúp đảm bảo chất lượng các cuộc hội thoại đồng thời tạo điều kiện cho vòng lặp cải tiến và triển khai nhanh chóng.

## Thách thức: Làm cho kiến thức đầu tư bất động sản trở nên dễ tiếp cận hơn
Lĩnh vực đầu tư bất động sản đặt ra nhiều thách thức cho cả nhà đầu tư mới lẫn những người có kinh nghiệm. Sự bất cân xứng thông tin tạo ra rào cản khi dữ liệu thị trường toàn diện thường đắt đỏ hoặc khó tiếp cận. Các quy trình đầu tư truyền thống mang tính thủ công, tốn thời gian, và đòi hỏi kiến thức sâu rộng về thị trường để điều hướng hiệu quả.

Đối với người tiêu dùng tại Tây Ban Nha và Úc, nhóm phát triển cần xây dựng một giải pháp có thể cung cấp lời khuyên đầu tư bất động sản chính xác, phù hợp với ngữ cảnh bằng tiếng Tây Ban Nha, đồng thời xử lý được các cuộc hội thoại phức tạp, nhiều lượt (multi-turn conversations) liên quan đến chiến lược đầu tư.

Hệ thống cần duy trì độ chính xác cao khi cung cấp phản hồi ở quy mô lớn, đồng thời không ngừng học hỏi và cải thiện thông qua tương tác của khách hàng. Quan trọng nhất, hệ thống phải có khả năng hỗ trợ người dùng trong mọi giai đoạn của hành trình đầu tư — từ giai đoạn khởi tạo (onboarding) đến khi hoàn tất giao dịch cuối cùng (final settlement), đảm bảo sự hỗ trợ toàn diện trong toàn bộ quá trình đầu tư.

## Tổng quan giải pháp
Chúng tôi đã xây dựng một giải pháp hoàn chỉnh end-to-end sử dụng AWS generative AI services, được thiết kế xoay quanh một multi-agent AI advisor với cơ chế continuous evaluation tích hợp. Hệ thống này cho phép luồng dữ liệu liền mạch từ khâu thu thập đến các cuộc hội thoại tư vấn thông minh, được giám sát chất lượng theo thời gian thực. Sơ đồ dưới đây minh họa kiến trúc tổng thể của giải pháp.

![System Architecture](/images/blog-3-1.jpeg)

Kiến trúc giải pháp bao gồm bốn lớp ảo (virtual layers), mỗi lớp đảm nhận các chức năng riêng trong thiết kế tổng thể của hệ thống.

## Data foundation layer
Lớp nền tảng dữ liệu cung cấp hạ tầng lưu trữ và truy xuất cho các thành phần của hệ thống:

* Amazon DynamoDB – Lưu trữ nhanh cho lịch sử hội thoại, các chỉ số đánh giá (evaluation metrics), và dữ liệu tương tác người dùng.
* Amazon Relational Database (Amazon RDS) for PostgreSQL – Cơ sở dữ liệu PostgreSQL lưu trữ dữ liệu quan sát từ LangFuse, bao gồm trace của LLM và các chỉ số độ trễ (latency metrics).
* Amazon Simple Storage Service (Amazon S3) – Data lake trung tâm lưu trữ tài liệu FAQ tiếng Tây Ban Nha, hướng dẫn đầu tư bất động sản, và tập dữ liệu hội thoại.
## Multi-agent AI layer
Lớp xử lý AI là trung tâm trí tuệ của hệ thống, điều khiển toàn bộ trải nghiệm hội thoại:
* Amazon Bedrock – Cung cấp foundation models (FMs) như LLMs và rerankers để vận hành các agent chuyên biệt.
* Amazon Bedrock Knowledge Bases – Công cụ tìm kiếm ngữ nghĩa (semantic search engine) với khả năng chia nhỏ dữ liệu theo ngữ nghĩa (semantic chunking) cho nội dung dạng FAQ.
* LangGraph – Điều phối luồng công việc giữa các agent (multi-agent workflows) và quản lý trạng thái hội thoại.
* AWS Lambda – AWS Lambda – Thực thi logic của multi-agent và truy xuất thông tin người dùng để cung cấp ngữ cảnh phong phú hơn.
## Continuous evaluation layer
Lớp hạ tầng đánh giá hỗ trợ giám sát và cải thiện chất lượng liên tục thông qua các thành phần sau:
* Amazon CloudWatch – Giám sát theo thời gian thực các chỉ số chất lượng, với hệ thống cảnh báo và quản lý ngưỡng tự động.
* Amazon EventBridge – Kích hoạt sự kiện thời gian thực khi hoàn tất hội thoại và thực hiện đánh giá chất lượng.
* AWS Lambda – Các hàm đánh giá tự động đo lường mức độ liên quan của ngữ cảnh (context relevance), độ xác thực của phản hồi (response groundedness), và độ chính xác mục tiêu (goal accuracy).
* Amazon QuickSight – Cung cấp bảng điều khiển tương tác (interactive dashboards) và phân tích để theo dõi các chỉ số tương ứng.
## Application and integration layer
Lớp tích hợp cung cấp các giao diện bảo mật cho việc giao tiếp bên ngoài:
* Amazon API Gateway – Cung cấp các endpoint API bảo mật cho giao diện hội thoại và webhook đánh giá.
## Kiến trúc cố vấn AI đa tác nhân
Cố vấn thông minh sử dụng một hệ thống multi-agent được điều phối thông qua LangGraph, hoạt động trong một Lambda function duy nhất, trong đó mỗi agent được tối ưu hóa cho một tác vụ cụ thể. Sơ đồ dưới đây minh họa luồng giao tiếp giữa các agent khác nhau trong Lambda function.
![System Architecture](/images/blog-3-2.png)

## Thành phần agent và chiến lược lựa chọn mô hình
Chiến lược lựa chọn mô hình của chúng tôi bao gồm quá trình thử nghiệm chuyên sâu nhằm khớp yêu cầu tính toán của từng thành phần với mô hình Amazon Bedrock hiệu quả nhất về chi phí. Chúng tôi đánh giá các yếu tố như chất lượng phản hồi, yêu cầu về độ trễ (latency), và chi phí trên mỗi token để xác định mô hình tối ưu cho từng loại agent. Mỗi thành phần trong hệ thống sử dụng mô hình phù hợp nhất với chức năng được chỉ định, như thể hiện trong bảng sau:


## Luồng hội thoại end-to-end
Quy trình xử lý hội thoại tuân theo một luồng làm việc có cấu trúc nhằm đảm bảo phản hồi chính xác và duy trì tiêu chuẩn chất lượng:
1. Truy vấn của người dùng được gửi qua API Gateway và được định tuyến đến router agent.
2. Router agent xác định specialized agent phù hợp dựa trên phân tích truy vấn.
3. Thông tin người dùng được truy xuất ngay từ đầu để cung cấp ngữ cảnh phong phú hơn; các truy vấn có tính chất chuyên sâu sẽ kích hoạt retriever truy cập Amazon Bedrock Knowledge Base.
4. Các specialized agents xử lý truy vấn dựa trên thông tin người dùng và ngữ cảnh có liên quan từ knowledge base.
định dạng và tạo phản hồi cuối cùng hiển thị cho người dùng với giọng điệu phù hợp.
5. Quá trình đánh giá song song (parallel evaluation) được thực hiện để đo lường mức độ liên quan ngữ cảnh, tính xác thực của phản hồi và độ chính xác của mục tiêu.
6. Dữ liệu hội thoại được lưu trữ trong DynamoDB để phục vụ phân tích và cải thiện sau này.
## Cấu hình Amazon Bedrock Knowledge Bases
Knowledge base sử dụng nhiều dịch vụ AWS khác nhau để tối ưu hóa hiệu năng:
* Data source – S3 bucket
* Chunking strategy – Semantic chunking được tối ưu cho nội dung dạng FAQ
* Embedding model – Cohere Embed Multilingual v3 để hiểu ngữ cảnh tiếng Tây Ban Nha
* Reranker – Cohere Rerank 3.5 để sắp xếp lại nội dung truy xuất bằng tiếng Tây Ban Nha
* Vector database – Amazon OpenSearch Serverless cho khả năng tìm kiếm ngữ nghĩa mở rộng (scalable semantic search)
## Trải nghiệm hội thoại mẫu
Hệ thống xử lý trơn tru các cuộc hội thoại tự nhiên bằng tiếng Tây Ban Nha. Ví dụ:

Usuario: “Hola, ¿qué es PropHero exactamente?”

Asistente: “¡Hola! PropHero es una plataforma que te permite crear, optimizar y crecer tu patrimonio inmobiliario delegando todo el proceso en nuestro equipo de profesionales…”

Usuario: “¿Y cómo funciona en la práctica?”

Asistente: “Es muy sencillo. Comenzamos con una sesión con tu Property Coach para definir tu estrategia de inversión personalizada…”
## Hệ thống đánh giá liên tục tích hợp
Hệ thống đánh giá liên tục được tích hợp trực tiếp vào kiến trúc, đóng vai trò như một thành phần cốt lõi. Cách tiếp cận này cho phép giám sát chất lượng theo thời gian thực song song với quá trình xử lý hội thoại.
### Các chỉ số đánh giá
Chúng tôi sử dụng các chỉ số đánh giá từ thư viện Ragas như sau:
* Context Relevance (0–1) – Đo lường mức độ liên quan của ngữ cảnh được truy xuất với truy vấn của người dùng, đánh giá hiệu quả của hệ thống RAG.
* Response Groundedness (0–1) – Đảm bảo phản hồi chính xác về mặt thông tin và được trích xuất từ dữ liệu chính thức của PropHero.
* Agent Goal Accuracy (0–1) – Chỉ số nhị phân thể hiện liệu phản hồi có giải quyết đúng mục tiêu đầu tư của người dùng hay không.
### Luồng đánh giá theo thời gian thực
Hệ thống đánh giá vận hành liền mạch trong kiến trúc hội thoại với các cơ chế sau:
* Amazon DynamoDB Streams triggers – Dữ liệu hội thoại ghi vào DynamoDB sẽ tự động kích hoạt Lambda function để thực hiện đánh giá qua Amazon DynamoDB Streams.
* Parallel processing – Các Lambda functions thực thi logic đánh giá song song với quá trình phản hồi người dùng.
* Multi-dimensional assessment – Mỗi cuộc hội thoại được đánh giá đồng thời theo ba chiều chính.
* Intelligent scoring with LLM-as-a-judge – đóng vai trò như một “LLM judge”, cung cấp các tiêu chí đánh giá tiêu chuẩn cho mọi hội thoại.
* Monitoring and analytics – CloudWatch thu thập các chỉ số từ quá trình đánh giá, trong khi QuickSight cung cấp bảng điều khiển trực quan để phân tích xu hướng.
Sơ đồ sau minh họa Lambda function chịu trách nhiệm cho quy trình đánh giá liên tục này.
![System Architecture](/images/blog-3-3.png)

## Các thông tin triển khai và thực tiễn tốt nhất
Hành trình phát triển được thực hiện trong 6 tuần cùng đội kỹ thuật của PropHero. Nhóm tiến hành thử nghiệm với nhiều tổ hợp mô hình khác nhau và đánh giá các chiến lược chunking bằng dữ liệu FAQ thực tế từ khách hàng. Quá trình này mang lại nhiều tối ưu kiến trúc giúp cải thiện hiệu năng hệ thống, giảm chi phí đáng kể và nâng cao trải nghiệm người dùng.
## Chiến lược lựa chọn mô hình
Cách tiếp cận của chúng tôi nhấn mạnh tầm quan trọng của việc lựa chọn mô hình phù hợp với từng tác vụ cụ thể. Bằng cách sử dụng Amazon Nova Lite cho các tác vụ đơn giản và Amazon Nova Pro cho các tác vụ suy luận phức tạp, hệ thống đạt được sự cân bằng tối ưu giữa chi phí và hiệu suất, đồng thời duy trì độ chính xác cao.
## Tối ưu hóa chunking và truy xuất
Kỹ thuật semantic chunking cho kết quả vượt trội so với các phương pháp hierarchical và fixed chunking trong nội dung dạng FAQ. Mô hình Cohere Rerank 3.5 giúp hệ thống chỉ cần sử dụng 10 chunk thay vì 20 mà vẫn duy trì độ chính xác, qua đó giảm độ trễ (latency) và chi phí vận hành.
## Khả năng đa ngôn ngữ
Hệ thống xử lý hiệu quả cả tiếng Tây Ban Nha và tiếng Anh bằng cách sử dụng các Foundation Models (FMs) hỗ trợ ngôn ngữ Tây Ban Nha trên Amazon Bedrock.
## Tác động kinh doanh
Cố vấn AI của PropHero mang lại giá trị kinh doanh rõ rệt:
* Tăng cường mức độ tương tác của khách hàng – Tỷ lệ goal accuracy đạt 90% đảm bảo khách hàng nhận được lời khuyên đầu tư bất động sản phù hợp và có thể hành động. Hơn 50% người dùng (và hơn 70% người dùng trả phí) đang chủ động sử dụng cố vấn AI.
* Hiệu quả vận hành – Việc tự động phản hồi các câu hỏi thường gặp giúp giảm 30% khối lượng công việc của bộ phận hỗ trợ khách hàng, cho phép nhân viên tập trung vào các nhu cầu phức tạp hơn.
* Khả năng mở rộng – Kiến trúc serverless tự động mở rộng để đáp ứng nhu cầu gia tăng của khách hàng mà không cần can thiệp thủ công.
* Tối ưu hóa chi phí – Chiến lược lựa chọn mô hình hợp lý giúp đạt hiệu năng cao trong khi giảm 60% chi phí AI so với việc sử dụng toàn bộ mô hình cao cấp.
* Mở rộng cơ sở khách hàng – Việc hỗ trợ ngôn ngữ Tây Ban Nha thành công giúp PropHero mở rộng sang thị trường người dùng nói tiếng Tây Ban Nha với năng lực bản địa hóa mạnh mẽ.
## Kết luận
Cố vấn AI của PropHero chứng minh cách AWS generative AI services có thể được sử dụng để xây dựng các conversational agents thông minh, nhận thức ngữ cảnh và mang lại giá trị kinh doanh thực tiễn. Bằng cách kết hợp kiến trúc agent mô-đun với hệ thống đánh giá mạnh mẽ, PropHero đã tạo ra một giải pháp vừa tăng cường tương tác khách hàng, vừa đảm bảo phản hồi chính xác và phù hợp. Đặc biệt, pipeline đánh giá toàn diện đóng vai trò quan trọng khi cung cấp các chỉ số rõ ràng để đo lường chất lượng hội thoại và định hướng cải tiến liên tục. Cách tiếp cận này đảm bảo rằng cố vấn AI sẽ tiếp tục phát triển và hoàn thiện theo thời gian. Để tìm hiểu thêm về cách xây dựng các cố vấn AI đa tác nhân với cơ chế đánh giá liên tục, vui lòng tham khảo các tài nguyên sau:

* Retrieve data and generate AI responses with Amazon Bedrock Knowledge Bases – Với Amazon Bedrock Knowledge Bases, bạn có thể triển khai tìm kiếm ngữ nghĩa với chiến lược chunking hiệu quả.
* LangGraph – Công cụ giúp bạn xây dựng các multi-agent workflows.
* Ragas – Cung cấp bộ chỉ số đánh giá LLM toàn diện bao gồm context relevance, groundedness, và goal accuracy như trong triển khai này.

Để tìm hiểu thêm về Generative AI Innovation Center, hãy liên hệ với account team của bạn.
