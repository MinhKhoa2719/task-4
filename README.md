DevOps là kết hợp của Development và Operations,xuất hiện năm 2009, là sự kết hợp của triết lý văn hóa, thực tiễn và những công cụ nhằm mục đích tăng tốc độ chuyển giao ứng dụng và dịch vụ của tổ chức: phát triển và cải tiến sản phẩm nhanh hơn các cơ sở hạ tầng truyền thống. Tốc độ này cho phép các tổ chức phục vụ khách hàng tốt hơn và cạnh tranh hiệu quả hơn trên thị trường.


DevOps khuyến khích tất cả thành viên vượt qua rào cản (từ góc độ nghề nghiệp, chuyên môn, bộ phận khác nhau …) và tạo ra một môi trường mà ở đó những người tạo ra phần mềm và những người hỗ trợ hoạt động của phần mềm làm việc cùng nhau trong một mối liên kết chặt chẽ và hài hòa, vì lợi ích chung của tập thể.

Về mặt khái niệm, CD và DevOps là hai thứ khác nhau, mặc dù chúng có ý nghĩa tương tự nhau, là tập trung vào những thay đổi nhỏ, nhanh chóng có giá trị với người dùng. CD là cách tiếp cận để tự động chuyển giao, tập trung vào việc develop, build, test, delivery sản phẩm nhanh chóng. Còn DevOps có phạm vi rộng hơn, và nó không phải công cụ, chẳng phải kỹ thuật, nó là một thứ “văn hóa”. Để đạt được thành công và hiệu quả, tốt nhất là sử dụng kết hợp cả hai: CD và DevOps. DevOps và Continuous Delivery chính là tương lai của phát triển phần mềm.



- Tìm hiểu CI, CD là gì?
- Tìm hiểu Github actions là gì?
- Tìm hiểu về 1 số price cần phải biết trong github ( GitHub Actions, GitHub Packages, Storage for Actions and Packages, Git LFS Data ) cho account free và account pro




# Tìm hiểu CI, CD là gì?
Quy trình CI/CD tham khảo
Có rất nhiều quy trình, công cụ khác nhau để ứng dụng CI/CD vào dự án. Nội dung của bài viết này dựa trên kinh nghiệm cho các dự án của mình triển khai cũng như đặc thù là các hệ thống web, và viết bằng PHP (PHP hoặc Python hoặc abc…không quá quan trọng trong ngữ cảnh chia sẻ về CI/CD).

Dưới đây là các bước thông thường của quá trình release tính năng trong một dự án thuộc hệ thống Teamcrop.
– Bước 1: [Manual] Khởi tạo repository và có branch default là master và dev. Cài đặt trên Gitlab 9.
– Bước 2: [Manual] Trừ owner ra, thì các coder sẽ push code tính năng lên branch dev
– Bước 3: [Auto] Hệ thống tự động thực hiện test source code, nếu PASS thì sẽ deploy tự động (rsync) code lên server beta.
– Bước 4: [Manual] Tester/QA sẽ vào hệ thống beta để làm UAT (User Acceptance Testing) và confirm là mọi thứ OK.
– Bước 5: [Manual] Coder hoặc owner sẽ vào tạo Merge Request, và merge từ branch dev sang branch master.
– Bước 6: [Manual] Owner sẽ accept merge request.
– Bước 7: [Auto] Hệ thống sẽ tự động thực hiện test source code, nếu PASS sẽ enable tính năng cho phép deploy lên production server.
– Bước 8: [Manual] Owner review là merge request OK, test OK. Tiến hành nhấn nút để deploy các thay đổi lên môi trường production.
– Bước 9: [Manual] Tester/QA sẽ vào hệ thống production để làm UAT và confirm mọi thứ OK. Nếu không OK, Owner có thể nhấn nút Deploy phiên bản master trước đó để rollback hệ thống về trạng thái stable trước đó.
– Bước 10: [Manual] Thắp nhang và hy vọng khách hàng không chửi rủa hoặc email complain.
CI/CD là một bộ đôi công việc bao gồm : CI (Continuous Integration)-(tích hợp liên tục) và CD (Continuous Delivery)-(phân phối liên tục)

# Bao Quát về CI :

- Giảm thiểu rủi ro nhờ việc phát hiện lỗi và fix sớm, tăng chất lượng phần mềm nhờ việc tự động test và inspect (đây cũng là một trong những lợi ích của CI, code được inspect tự động dựa theo config đã cài đặt, đảm bảo coding style, chẳng hạn một function chỉ được dài không quá 10 dòng code …)
- Giảm thiểu những quy trình thủ công lặp đi lặp lại (build css, js, migrate, test…), thay vì đó là build tự động, chạy test tự động
- Sinh ra phần mềm có thể deploy ở bất kì thời gian, địa điểm

# Bao Quát về CD

- CI là quy trình để build và test tự động, thì CD nâng cao hơn một chút, bằng cách triển khai tất cả thay đổi về code (đã được build và test) đến môi trường testing hoặc staging. Continuous Delivery cho phép developer tự động hóa phần testing bên cạnh việc sử dụng unit test, kiểm tra phần mềm qua nhiều thước đo trước khi triển khai cho khách hàng (production).
- Những bài test này bao gồm UI testing, load testing, integration testing, API testing… Nó tự động hoàn toàn quy trình release phần mềm.

- CD là yêu cầu cho việc thực hiện DevOps. Chỉ khi code được chuyển giao liên tục, chúng ta mới có thể tự tin rằng những thay đổi từ code sẽ phục vụ cho khách hàng sau chỉ vài phút với một nút ấn.

# Tìm hiểu Github actions là gì?               

Các chức năng chính của Github như Pull Requests, Issues, hay là code nhưng ít khi chúng ta để ý đến các chức năng khác của Github

chức năng Actions của Github và sử dụng nó đến deploy dự án lên Github Pages. Vậy Github Actions là gì? Sử dụng nó như thế nào?

# Github Actions là gì?
- Github Actions cho phép chúng ta tạo workflows vòng đời phát triển phần mềm cho dự án trực tiếp trên Github repository của chúng ta
- Github Actions giúp chúng ta tự động hóa quy trình phát triển phần mềm tại nơi chúng ta lưu trữ code và kết hợp với pull request và issues. 
- Chúng ta có thể viết các tác vụ riêng lẻ, được gọi là các actions và kết hợp các actions đó lại với nhau để tạo ra một workflow theo ý của chúng ta. 
- Workflow là các tiến trình tự động mà bạn có thể thiết lập trong repository của mình để build, test, publish package, release, hoặc deploy dự nào trên Github
- Với Github Actions chúng ta có thể tích hợp continuous integration (CI) và continuous deployment (CD) trực tiếp trên repository của mình
Ví Dụ sử dụng Github Actions để auto deploy một dự án ReactJs lên gihub pages
.
.






