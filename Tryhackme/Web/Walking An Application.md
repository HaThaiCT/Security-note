

## Exploring a website

+ Khám phá tất cả các pages/ khu vực/ tính năng của website đó
Ví dụ : 

|                         |                       |                                                                                                                                                           |
| ----------------------- | --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Feature**             | **URL**               | **Summary**                                                                                                                                               |
| Home Page               | /                     | This page contains a summary of what Acme IT Support does with a company photo of their staff.                                                            |
| Latest News             | /news                 | This page contains a list of recently published news articles by the company, and each news article has a link with an id number, i.e. /news/article?id=1 |
| News Article            | /news/article?id=1    | Displays the individual news article. Some articles seem to be blocked and reserved for premium customers only.                                           |
| Contact Page            | /contact              | This page contains a form for customers to contact the company. It contains name, email and message input fields and a send button.                       |
| Customers               | /customers            | This link redirects to /customers/login.                                                                                                                  |
| Customer Login          | /customers/login      | This page contains a login form with username and password fields.                                                                                        |
| Customer Signup         | /customers/signup     | This page contains a user-signup form that consists of a username, email, password and password confirmation input fields.                                |
| Customer Reset Password | /customers/reset      | Password reset form with an email address input field.                                                                                                    |
| Customer Dashboard      | /customers            | This page contains a list of the user's tickets submitted to the IT support company and a "Create Ticket" button.                                         |
| Create Ticket           | /customers/ticket/new | This page contains a form with a textbox for entering the IT issue and a file upload option to create an IT support ticket.                               |
| Customer Account        | /customers/account    | This page allows the user to edit their username, email and password.                                                                                     |
| Customer Logout         | /customers/logout     | This link logs the user out of the customer area.                                                                                                         |
## Viewing the page source

+ Page source là đoạn mã nguồn mà người bình thường có thể xem được của trang web, được cấu tạo bởi HTML, CSS, JS
+ Nhấp chuột phải, chọn View Page Source trên trình duyệt
+ Luôn tìm kiếm các mọi đường dẫn trong source code, nó có thể dẫn tới 1 nơi hữu ích nào đó

## Developer Tools - Inspector

+ Hỗ trợ trực tiếp việc đang hiển thị những gì trên trang web
+ Có thể sửa CSS style, HTML và cả JS để trang web hiển thị theo ý muốn

## Developer Tools - Debugger

+ Dùng để developer debug Javascript nhưng là phương tiện hữu ích để hacker đào sâu vào mã Javascript
+ Thường là Sources hoặc là Debugger tùy trình duyệt

## Developer Tools - Network

+ Dùng để xem các gói tín gửi đi của trình duyệt và response của chúng
+ Có thể dùng để gửi 1 message nào đó