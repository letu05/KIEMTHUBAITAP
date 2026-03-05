JMeter Performance Testing Report
1. Mục tiêu

Bài thực hành này nhằm:

Hiểu cách sử dụng Apache JMeter để kiểm thử hiệu năng website.

Thiết kế nhiều kịch bản kiểm thử (Thread Group) với các tham số khác nhau.

Phân tích các chỉ số hiệu năng như:

Response Time

Throughput

Error Rate

Website được sử dụng để kiểm thử:

https://vnexpress.net
 của VnExpress

2. Thiết lập môi trường

Công cụ sử dụng:

Apache JMeter 5.6.3

Cấu hình cơ bản:

HTTP Request Defaults

Protocol: https

Server Name: vnexpress.net

Listeners sử dụng:

View Results Tree

Summary Report

3. Kịch bản kiểm thử
3.1 Thread Group 1 – Kịch bản cơ bản
Cấu hình
Tham số	Giá trị
Users (Threads)	10
Loop Count	5
Request	HTTP GET
Trang kiểm thử	Trang chủ

URL:

https://vnexpress.net
Kết quả
Chỉ số	Giá trị
Samples	50
Average Response Time	2441 ms
Min	690 ms
Max	5184 ms
Throughput	3.7 requests/sec
Error Rate	0%
Nhận xét

Website phản hồi khá ổn định.

Không có lỗi trong quá trình kiểm thử.

Thời gian phản hồi trung bình khoảng 2.4 giây.

3.2 Thread Group 2 – Kịch bản tải nặng
Cấu hình
Tham số	Giá trị
Users	50
Ramp-up Period	30 giây
Requests	2

Các request:

Trang chủ

https://vnexpress.net

Trang con

https://vnexpress.net/tin-tuc-24h
Kết quả
Trang	Samples	Avg Response	Min	Max
Trang chủ	150	6547 ms	354	18008
Trang con	150	5877 ms	297	14069

Tổng kết:

Chỉ số	Giá trị
Total Samples	300
Average Response	6212 ms
Throughput	4.8 req/sec
Error Rate	0%
Nhận xét

Khi số lượng người dùng tăng lên 50, thời gian phản hồi tăng đáng kể.

Thời gian trung bình khoảng 6.2 giây.

Website vẫn hoạt động ổn định và không phát sinh lỗi.

3.3 Thread Group 3 – Kịch bản tùy chỉnh
Cấu hình
Tham số	Giá trị
Users	20
Duration	60 giây
Requests	2 trang con

Trang kiểm thử:

Trang công nghệ

https://vnexpress.net/so-hoa

Trang thể thao

https://vnexpress.net/the-thao
Kết quả
Trang	Samples	Avg Response	Min	Max
Trang công nghệ	47	12935 ms	3300	37641
Trang thể thao	42	13267 ms	3236	29678

Tổng:

Chỉ số	Giá trị
Total Samples	89
Average Response	13092 ms
Throughput	1.3 req/sec
Error Rate	0%
Nhận xét

Thời gian phản hồi tăng cao (khoảng 13 giây).

Điều này có thể do:

nội dung trang lớn

nhiều hình ảnh

tải tài nguyên từ nhiều server

4. So sánh các kịch bản
Kịch bản	Users	Avg Response	Throughput
Basic	10	2441 ms	3.7/sec
Heavy Load	50	6212 ms	4.8/sec
Custom	20	13092 ms	1.3/sec

Nhận xét:

Khi tăng số lượng người dùng, thời gian phản hồi tăng lên.

Throughput tăng ở mức tải lớn nhưng thời gian phản hồi cũng tăng theo.

Website vẫn ổn định với Error Rate = 0%.

5. Kết luận

Thông qua bài kiểm thử bằng Apache JMeter, có thể rút ra:

Website VnExpress xử lý tốt với tải thấp.

Khi số lượng người dùng tăng, response time tăng đáng kể.

Tuy nhiên hệ thống vẫn không xảy ra lỗi trong quá trình kiểm thử.

Kiểm thử hiệu năng giúp:

Đánh giá khả năng chịu tải của hệ thống

Phát hiện điểm nghẽn hiệu năng

Hỗ trợ tối ưu hệ thống trước khi triển khai thực tế
