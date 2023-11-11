# About this Challenge
- Link: [Có thể sẽ bị đóng về sau](http://caterpie_c3488068a00808d7281f030ac3433427.ctf.night-wolf.io/index)
- Mô tả: Trong hàng nghìn người đăng ký, không ai biết ta là ai :|| thử tìm xem ta là ai nhé
- Hint: Admin Right
# WhoamI 
- Vào web của đề bài ta có một login form, lúc đầu. Nhưng đương nhiên ta cần phải register cái đã. Form register khá cứng về type của từng box, có mỗi Name là khá tự do nên tôi nghĩ có thể nó sẽ tận dụng được
- Sau khi reg xong thì tôi login vào như bình thường thôi, thứ đập thẳng vào mắt tôi là một bảng tên những người đã đăng ký (may quả mình không set thông tin thật)

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/e4884cd9-cedb-47f0-b3b0-2c8683012a07)
- Check source code cái nào

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/4df111e9-6980-404a-9800-39d69b7ab639) <br>Có một cái comment là flag ở đâu đó quanh đấy. Nếu tôi đọc đúng thì cái ```console.log(data.flag)``` sẽ được thực thi mỗi khi login vào (hiện ở console nhé :||)
- Tuy nhiên khi tôi kiểm tra thì những gì nó in ra là permession denied

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/abe420d2-80ce-4c2c-9e5b-1eb0676989db) <br> Có nghĩa là ta cần một quyền nhất định để lấy flag
- Nãy thì trong source-code còn có một path trông có vẻ thú vị ![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/ddfff80e-aaa1-49a9-a304-eb035ab710c5)
- Truy cập vào path này, ta nhận ra ngoài các thông tin cơ bản thì còn có một thông tin nữa là ```"isAdmin"=fasle```, vậy kết luận lại là ta cần phải sửa nó thành true ![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/6ee9b897-f3fe-4310-9ae6-de5d58cfd7f9)
- Biết gì không :|| tôi đã nói rằng name của web này được đặt rất tự do, giờ thì hãy thử tận dụng nó nào
- Hình như ta có thể tận dụng được ```name```, nhưng mấy cái ngoặc của nó khá rối nên tôi quyết định dùng Burp để xử lý phần này
- Việc ta cần làm chỉ đơn giản là thêm một dòng ```"isAdmin":true``` vào request thôi ![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/40fae53f-e3de-43a4-8722-3e5c4a12dd5e)
- Sau khi hoàn thành hãy thử đăng nhập lại và bạn sẽ lấy được flag trong console hay ở path ```/api/v1/flag```
