# Async
### 1.1 Sync vs Async
#### * Sync code (code đồng bộ) là gì ? <br>
Code đồng bộ thực thi các câu lệnh từng dòng một từ trên xuống,chờ cho câu lệnh trước hoàn thành mới thực hiện các câu lệnh tiếp theo . Khi thực thì một hàm, code bất đồng bộ sẽ chờ đến khi hàm đó trả về giá trị mới thực hiện tiếp câu lênh bên dưới
#### * Async code (code bất đồng bộ) là gì ? <br>
Code bất đồng bộ không chờ cho hàm được trả về mà vẫn tiếp tục thực thi các câu lệnh bên dượi
#### * Theo em JavaScript là ngôn ngữ đồng bộ hay bất đồng bộ <br>
Javascript là ngôn ngữ bất đồng bộ
### 1.2 setTimeout
#### * Định nghĩa hàm setTimeout <br>
- Hàm setTimeout gọi một hàm hoặc tính tóan giá trị biểu thức sau một thời gian chờ tính theo milisecond <br>
- setTimeout không phải là hàm có sẵn trong V8 core, nó được cung cấp bởi browser <br>
- setTimeout  vói n milisecond chỉ bảo đảm thời gian chờ thối thiểu là n, chứ không bảo đảm hàm sẽ được thực thi sau n milisecond, thời gian chờ có thể lâu hơn
#### * Set đoạn code sau, hãy mô tả chính xác những gì xảy ra và kết quả in ra là gì ? <br>
```
console.log('Hi');

setTimeout(function () {
  console.log('there');
}, 1000);
```
- Hàm console.log('Hi') được đưa vào call stack, chương trình thực thi hàm console.log và in ra string "Hi", hàm pop ra khỏi stack <br>
- setTimeout đưa vào call stack, chuyển qua cho browser xứ lý, chờ 1s, sau thời gian chờ đẩy function console.log('there'); vào callback queue.
- Khi call stack trống, event loop đẩy callback function vào stack, thực thi hàm console.log('there'),in ra string 'there',  <br>
- Kết quả in ra là 'Hi', 1 giây sau in ra 'there'
```
console.log('Hi');

setTimeout(function () {
  console.log('there');
}, 0);
console.log('Hi again');
```
- Hàm console.log('Hi') được đưa vào call stack, chương trình thực thi hàm console.log và in ra string "Hi", hàm pop ra khỏi stack <br>
- setTimeout đưa vào call stack, chuyển qua cho browser, browser gọi hàm setTimeout, function console.log('there')được đưa vào vào callback queue ngay vì thời gian chờ bằng 0s
- Cùng lúc này, hàm console.log('Hi again') được đưa vào call stack, chương trình thực thi hàm console.log và in ra string "Hi again", hàm pop ra khỏi stack <br>
- Khi call stack trống, event loop đẩy callback function vào stack, thực thi hàm console.log('there'),in ra string 'there',<br>
- Kết quả in ra là 'Hi', 'Hi again' và 'there'
#### * Từ ví dụ trên em có nhận xét gì? <br>
- Call stack là dạng câu trúc dữ liệu thể hiện lượt mà func được thực thi
- setTimeout và 1 số hàm khác không nằm trong V8 mà được cung cấp bởi browser, vì thế khi gọi sec do broswer xử lý, vì thế cho nên các callback func của các hàm này sau khi được xử lý xong sẽ chò ở callback queue, khi call stack trống sẽ được đẩy vào để thực thi theo thứ tự First In First Out

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
Thứ tự (1) => (3) => (2) <br>
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
- Khi người dùng click vào button, function callback trong hàm addEventListener sẽ được gọi và đẩy vào call stack, hàm này sẽ gọi hàm setTimeout, nên hàm setTimeout cũng được đẩy vào callstack. Do settimeout không phải là hàm của V8 nên nó sẽ được đẩy sang cho Event Table. Web ÁP sẽ thực thi hàm setTimeout và bắt đều đếm thời gian chờ, Sau khi chờ hết thời gian 1s, callback func của setTimeout sẽ được đầy vào Task Queue. Khi Event Loop thấy callstack rỗng mà có hàm đang chờ ở task queue thì nó sẽ đẩy hàm vào call stack,Sau đó hàm được thực thi
#### * Theo em những điểu bất lợi của callbacks là gì ? liên quan đến: code readability, code security, handle errors code, code reusability

### 1.5 Promises
#### Tìm hiểu về Promises: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
#### What is a future value ?
#### Promise value ?
#### Promise Events ?
#### How to get Promise value?
#### How to handle error in Promise ?
#### How to chain Promises ?
#### Promise.all
#### Promise.race
#### finally
