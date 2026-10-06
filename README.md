TƯ VẤN KIẾN TRÚC PHẦN MỀM: TẦM QUAN TRỌNG CỦA KIẾN TRÚC & THUỘC TÍNH CHẤT LƯỢNG


Câu 1: Tại sao trước khi bắt đầu một dự án, việc chọn kiến trúc lại là bước sống còn?

Kiến trúc phần mềm (Sortware Architecture) là bộ khung cơ bản của các thành phần mềm, mối quan hệ giữ chúng và các nguyên tắc thiết kế chi phối toàn bộ hệ thống. Đối với một fujw án --đặc biết starup -- đấy là một bước sống còn vì:
- chi phí thay đổi tỷ lệ thuận với thời gian (Cost of Change): Theo định luất phát triển phần mềm, sửa một lỗi kiến trúc ở giai đoạn phân tích chỉ tốn vào giờ, sửa khi đang code tốn vài ngày; nhưng sửa khi đã có hàng triệu người dùng sẽ tốn hàng tháng trời cùng nguy cơ đập đi xây lại (rewrite) toàn bộ.
- Định hình các thuộc tính phi chức năng (Non-Functional Requirements): Tính năng nghiệp vụ (Functional) có thể code thêm bằng bất kỳ ngôn ngữ hay mô hình nào, nhưng các yếu tố như độ chịu tải, bảo mật, thời gian phản hồi lại do chính kiến trúc quyết định.
- Tối ưu hóa nguồn lực và tổ chức team: Kiến trúc phần mềm quyết định cách phân chia công việc (Định luật Conway - Conway's Law). Chọn sai kiến trúc (ví dụ: team 3 người nhưng chia 20 microservices) sẽ làm kiệt quệ tài nguyên vận hành trước khi sản phẩm kịp tìm được chỗ đứng trên thị trường (Product-Market Fit).

- Câu 2: Liệt kê các loại kiến trúc phần mềm mà bạn biết (Ít nhất 3 loại).
- Monolithic (Đơn khối):
-- Đặc điểm cốt lõi: Toàn bộ chức năng (UI, Business Logic, Data Access) đóng gói chung trong một khối mã nguồn và chạy trên một tiến trình duy nhất.
-- Ưu điểm: Dễ phát triển ban đầu, triển khai nhanh, dễ debug và kiểm thử toàn cục.
-- Nhược điểm: Khó mở rộng từng phần, một lỗi nhỏ có thể làm sập toàn bộ hệ thống, thời gian build/deploy lâu khi codebase phình to.
-- Trường hợp áp dụng: Rất phù hợp cho MVP giai đoạn đầu của startup để nhanh chóng kiểm chứng thị trường.
- Microservices (Vi dịch vụ):
-- Đặc điểm cốt lõi: Chia nhỏ hệ thống thành nhiều dịch vụ độc lập theo nghiệp vụ (Domain-driven), giao tiếp qua API (REST, gRPC) hoặc Message Broker.
-- Ưu điểm: Khả năng mở rộng độc lập từng dịch vụ, linh hoạt công nghệ, cô lập lỗi tốt.
-- Nhược điểm: Phức tạp trong điều phối, tính nhất quán dữ liệu phân tán (Distributed Transactions), chi phí hạ tầng và vận hành cao.
-- Trường hợp áp dụng: Hệ thống lớn, traffic cao, quy mô công ty có nhiều đội ngũ phát triển độc lập.
- Event-Driven (Kiến trúc hướng sự kiện):
-- Đặc điểm cốt lõi: Các thành phần giao tiếp bất đồng bộ thông qua việc sinh ra (Publish) và tiêu thụ (Consume) các sự kiện (Events) qua hàng đợi (Kafka, RabbitMQ).
-- Ưu điểm: Khớp nối lỏng (Decoupled), hiệu năng phản hồi cao, xử lý luồng dữ liệu thời gian thực rất tốt.
-- Nhược điểm: Khó theo dõi luồng dữ liệu (traceability), xử lý lỗi phức tạp, dữ liệu chỉ đảm bảo tính nhất quán cuối cùng (Eventual Consistency).
-- Trường hợp áp dụng: Hệ thống tài chính, thanh toán, xử lý đơn hàng e-commerce, thông báo theo thời gian thực.
- Layered / N-Tier Architecture (Kiến trúc phân tầng): 
-- Đặc điểm cốt lõi: Phân chia hệ thống thành các tầng riêng biệt: Presentation, Business Logic, Persistence, Database.
-- Ưu điểm: Cấu trúc rõ ràng, dễ bảo trì, phân chia trách nhiệm (SoC) tốt.
-- Nhược điểm: Dễ rơi vào tình trạng các tầng bị phụ thuộc cứng vào nhau, suy giảm hiệu năng qua nhiều tầng trung gian.
-- Trường hợp áp dụng: Các ứng dụng quản lý doanh nghiệp vừa và nhỏ, RESTful APIs truyền thống.

Câu 3: Hãy liệt kê và giải thích các thuộc tính chất lượng (Quality Attributes) của phần mềm (Ví dụ: Scalability, Availability, Maintainability...).
Thuộc tính chất lượng là các thước đo đánh giá một hệ thống vận hành tốt đến mức nào trong các điều kiện thực tế:

Scalability (Khả năng mở rộng):

- Ý nghĩa: Khả năng hệ thống xử lý khối lượng công việc tăng lên (traffic, dữ liệu) bằng cách bổ sung thêm tài nguyên.

- Phân loại: Mở rộng theo chiều dọc (Vertical Scaling - nâng cấp CPU/RAM) và chiều ngang (Horizontal Scaling - thêm máy chủ/node chạy song song).

Availability (Tính sẵn sàng):

- Ý nghĩa: Tỷ lệ phần trăm thời gian hệ thống hoạt động bình thường và người dùng truy cập được (thường đo bằng các chữ số 9, ví dụ 99.9% uptime).

- Giải pháp: Dự phòng (Redundancy), cân bằng tải (Load Balancing), tự động phục hồi sự cố (Failover).

Maintainability (Khả năng bảo trì):

- Ý nghĩa: Mức độ dễ dàng khi sửa lỗi, tối ưu hiệu năng hoặc thêm tính năng mới mà không làm gãy các phần khác.

- Yếu tố quyết định: Codebase phân tầng rõ ràng, giảm thiểu khớp nối (Low Coupling - High Cohesion), tuân thủ Clean Code và có kiểm thử tự động (Unit/Integration Test).

Performance (Hiệu năng):

- Ý nghĩa: Tốc độ phản hồi (Latency) và năng lực thông lượng (Throughput) của hệ thống khi xử lý một lượng yêu cầu trong một đơn vị thời gian.

Security (Tính bảo mật):

- Ý nghĩa: Năng lực bảo vệ dữ liệu và chức năng khỏi các truy cập trái phép, tấn công mã độc, đảm bảo các yếu tố CIA (Confidentiality, Integrity, Availability).