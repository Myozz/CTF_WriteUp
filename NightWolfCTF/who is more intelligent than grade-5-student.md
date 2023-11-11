# Giới thiệu
- Link: [Có thể bị đóng sau này](http://charmander_4d9b932ef24aab875891e791b6c340c4.ctf.night-wolf.io/)
- Mô tả: Vượt qua thử thách để lấy flag :||
- Hint: Ai thông minh hơn học sinh lớp 6 :)) (hint này vui thôi)

# Ai thông minh hơn học sinh lớp 5
- Đầu tiên tôi chỉ đơn giản là cứ làm như bình thường thôi, cho đến khi gặp câu Việt Nam vô địch năm nào thì tắc tịt :))
- Tôi thử check source code thì có một file là ```secret.css```, và xem chừng nó một cái gì đó được mã hoá bằng sha-256

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/eaed6392-adaf-4b75-9d70-5f7814beecda)
- Tôi thử dùng Burp măng để lấy request của câu hỏi thì thấy có một đoạn token và tôi khá chắc chắn ta có thể thử encrypt nó :||

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/e250e0f6-4f36-4417-b7a4-f4296c6161c0)

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/4a508ea6-44a4-45ab-b40d-aa897f812120)

- Hmm :)) có vẻ nó không đúng với ý tôi cho lắm, tôi thử nhập output vào thì phải làm lại, thôi thì ta xử lý lại từ lv1 vậy
- Tôi vừa nghĩ ra một hướng đi mới :||, trong request có ghi là level=<token>, có nghĩa là token có thể là ```1```, ```level1```, ```level 1``` hay đại khái vậy. Tôi đã thử và nó kì thực đúng như vậy

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/6b3c2558-b328-41f8-9ae5-039e14d85b62)

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/b1f6cd83-600a-4bef-8ebc-53438f125238)
<br> Cái này thực sự để là 1 thì hợp lí hơn ấy :||
- Có thể level 5 cũng tương tự, tôi sẽ hash thử ```level8``` và thay thế vào request xem nhé

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/13dfc596-fb4e-4f07-ae26-573a8d7b4f16)
- Mọi thứ có vẻ vẫn không đúng lắm, tôi thử tiếp là ```level6``` thôi và lần này thì tôi đã lên được level 6

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/7ba54fbc-4384-4027-be3e-1ee0120eed44)
- Lên level 6 có vẻ cách trước đó sẽ không còn hoạt động nữa, tôi cũng đã thử rồi. Check qua source code của level 6 thì cũng không có gì khác biệt
- Tôi cũng đã check metadata của cái cờ nhưng cũng chả có gì :|| tôi đã kẹt khá lâu ở đoạn này
- Còn nếu chọn rồi bấm trả lời thì ta lại được một vé về level 5, tuyệt vời :))
- Tôi quay lại level 6 rồi thử check request của nút trả lời, tôi thấy token bị thay đổi :|| đó là lí do tôi về level 5. Tôi cố chấp chèn lại token của level 6 vào đó <br>
![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/d2a63cc0-ec03-45bd-a472-d6b1186a563a)
<br> và kết quả là ![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/22e87a9c-7626-46fb-96b3-62875b2d5687)
