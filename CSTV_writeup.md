**FOR1-stego**

* Tải file có tên Lost.docx về và em kiểm tra thì biết file này loại file word, mở ra xem thì bên trong có chứa 1 ảnh như này:
![image2](https://hackmd.io/_uploads/rJmKdKt_T.jpg)

* Và em nghĩ là flag sẽ được giấu trong ảnh này nhưng sau khi dùng tool [www.aperisolve.com/](
https://) và các lệnh như strings,exftool,hexeditor.. để kiểm tra nhưng không thấy gì khả nghi cả .
* Lúc này thì em quay lại file Lost.docx để kiểm tra kỹ hơn và dùng lệnh binwalk để xem có ẩn chứa gì không thì thấy nhưng file như này:
![Screenshot 2024-01-08 203025](https://hackmd.io/_uploads/HyaeGtYOT.png)

* Em tiến hành trích xuất ra và sau 1 hồi check thì em phát hiện ra có 2 ảnh cùng này trong 1 thư mục nhưng chỉ có 1 ảnh xem được còn 1 ảnh bị lỗi và em đi kiểm tra mã hex thì thấy phần chữ kí file là PK:
 ![Screenshot 2024-01-08 203957](https://hackmd.io/_uploads/B1s-ftKdT.png)

* Em đổi đuôi mở rộng lại thành .zip và extrat ra thì cần có passwword , thì em nghĩa ngay đến việc brute fouce và em sẽ dùng john để crack:
 ![Screenshot 2024-01-08 204608](https://hackmd.io/_uploads/SJymfYtuT.png)

* Đã thành công có được mật khẩu là: loveyou và mở file zip đó ra có 1 ảnh bên trong và em tiến hành dùng tool [
https://www.aperisolve.com/](https://) thì xuống đến phần steghide thì thấy có 1 file flag.txt:
 ![Screenshot 2024-01-08 205045](https://hackmd.io/_uploads/ryWBMYYd6.png)

* Em tiến hành downloads về thì có được flag
**flag**: hackathon{bbc649da49b02570835df50fd173bff7d4933f07}

**FOR2-Network**
 
*  Sau khi tải về 1 file pcap và dùng wirehark để xem các gói tin mạng:
1. *  Đầu tiên là em vào statistics->protocol hierarchy để xem là giao thức nào là chủ yếu:
![Screenshot 2024-01-08 213605](https://hackmd.io/_uploads/HyruuKY_p.png)
lúc này em sẽ check theo thức tự số lượng từ cao xuống thấp.
2. Sau một hồi follow thì em thấy có 1 vài file get đến sever, trong đó có 1 file là setup.exe có chứa malware sau 1 hồi khai thức thi em thấy không khả lắm chẳng thấy được manh mối gì
3. Tiếp tục em check protocol dns lướt xem packet list thì đó điều khả nghi là có rất nhiều data truy vấn được đẩy lên sever và đánh theo số theo thứ tự:
![Screenshot 2024-01-08 215243](https://hackmd.io/_uploads/SyYXAYK_a.png)
và em dùng tshark để lấy nhưng dòng data đó về : tshark -r capture.pcap -Y "dns and ip.dst == 192.168.95.134" -T fields -e dns.qry.name > dataa  , ta được kết quả là :
![Screenshot 2024-01-08 220431](https://hackmd.io/_uploads/Hk0cJ5K_6.png)
3.1. Em sẽ dùng code để xử lí mấy cái rác ở đầu và cuối:
```s=""
with open(r'C:\Users\Admins\Desktop\python_code\test-code_with_file\dns.txt','r') as file:
   
   for i in file:
       r=i.split(".")
       s+=r[1]
with open(r'C:\Users\Admins\Desktop\python_code\test-code_with_file\dns.txt','w') as file:
    file.write(s)  
```
3.2. Ta được các đoạn mã hex sau
![Screenshot 2024-01-08 221257](https://hackmd.io/_uploads/HJRmbqYua.png)
,tiếp tục ta sẽ lên cyberchef [
https://gchq.github.io/CyberChef/](https://) để decode thì ta nhận được 1 file có phần chữ kí là PK:
![Screenshot 2024-01-08 221859](https://hackmd.io/_uploads/rkY9G9Kd6.png)
Tiến hành downloads về mở ra thì có được flag 

**Flag** : CSTV_2023_{ba69f4c8c869295a9a8024b32a177bc63a942ffd} 









