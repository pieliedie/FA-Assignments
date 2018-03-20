# Async
### 1.1 Sync vs Async
#### * Sync code (code đồng bộ) là gì ? <br>
Code đồng bộ thực thi các câu lệnh từng dòng một từ trên xuống,chờ cho câu lệnh trước hoan thành mới thực hiện các câu lệnh tiếp theo . Khi thực thì một hàm, code bất đồng bộ sẽ chờ đến khi hàm đó trả về giá trị mới thực hiện tiếp câu lênh bên dưới
#### * Async code (code bất đồng bộ) là gì ? <br>
Code bất đồng bộ không chờ cho hàm được trả về mà vẫn tiếp tục thực thi các câu lệnh bên dượi
#### * Theo em JavaScript là ngôn ngữ đồng bộ hay bất đồng bộ <br>

### 1.2 setTimeout
#### * Định nghĩa hàm setTimeout <br>
#### * Set đoạn code sau, hãy mô tả chính xác những gì xảy ra và kết quả in ra là gì ? <br>
```
console.log('Hi');

setTimeout(function () {
  console.log('there');
}, 1000);
```
```
console.log('Hi');

setTimeout(function () {
  console.log('there');
}, 0);
console.log('Hi again');
```
#### * Từ ví dụ trên em có nhận xét gì? <br>
### 1.3 Event Loop
### 1.4 Callbacks
#### * Người ta nói callback functions đóng gói tính liên tục của chương trình. Theo em chương trình dưới sẽ được chạy liên tục ra sao? Ví dụ (1) => (2) => (3) 
```
// (1)
setTimeout(function () {
  // (2)
}, 1000);
// (3)
```
#### * Nested/Chained Callbacks
Set đoạn code sau, khi người dùng click vào btn thì điều gì xảy ra?
```
// (0)
var btn = document.getElementById('btn');
btn.addEventListener('click', function () {
  // (1)
  setTimeout(function () {
    // (2)
  }, 1000);
  // (3)
});
```
#### * Theo eo những điểu bất lợi của callbacks là gì ? liên quan đến: code readability, code security, handle errors code, code reusability
