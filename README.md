# # Analytics Google with React js project 


## Overview

Google Analytics cung cấp số liệu thống kê và các phân tích cơ bản để bạn có thể tối ưu hóa công cụ tìm kiếm ( SEO ) và các mục đích tiếp thị. Giúp bạn có thể dễ dàng xác định được lưu lượng truy cập trang web, tỷ lệ chuyển đổi đến tỷ lệ thoát của trang web và nhiều hơn nữa. Chính vì tầm quan trọng của nó là vậy nên ở một số framework hay CMS nó đã được tích hợp sẵn => việc sử dụng nó hết sức đơn giản. Vậy đối với một library mới và mạnh như thằng React js thì thế nào?

![google-analytics-la-gi](https://user-images.githubusercontent.com/13729049/60029973-59775b80-96cc-11e9-92d7-dd95acc22369.jpg)

## Setup

- Trước tiên ta tạo một demo với create-app-react
```bash
 create-react-app analytics_google_react
```
- [Branch source](https://github.com/khacthe/analytics_google_react/pull/1/files)

- Bước tiếp theo ta cần cài đặt react-ga package

```bash
 npm i react-ga -S
```
react-ga giúp ta kết nối Analytics Google với React.

Bước tiếp theo ta cần đăng nhập vào google analytics: https://analytics.google.com -> lấy giá trị trackingId

- Init module application

```ruby
import ReactGA from 'react-ga';
import auth from './auth.ts';
const trackingId = "US-1234567890-1"; // Giá trị trackingId khi tạo tài khoản analytics
ReactGA.initialize(trackingId);
ReactGA.set({
  userId: auth.currentUserId(),
})

```

## Tracking Event
+ Ở đây ta giả sử theo giỏi sự kiện đăng kí và login user ở trang web

```ruby
ReactGA.event({
  category: "Đăng kí",
  action: "Người dùng click đăng kí",
});


ReactGA.event({
  category: 'Login',
  action: 'Người dùng login',
});

```
react-ga còn hỗ trợ thêm nhiều options

```ruby
args.category: String type
args.action : String type
args.label: String type
args.value: Int type
args.nonInteraction: Boolean type
args.transport: Support

```


Khi bất kì người dùng nào ấn click vào button đăng kí hoặc login thì dừ liệu google analytics sẽ cập nhật và hiểu thì cho người quản trị.
![sheet](https://user-images.githubusercontent.com/13729049/60030002-685e0e00-96cc-11e9-9fb0-51e9746b521a.png)
Vậy làm thế nào để tracking toàn bộ page của trang web ?

## Tracking Page View

Ở đây chúng ta sẽ cần sử dụng đến react-router và history giúp cho việc tracking dễ dàng hơn

Install package

```ruby
npm i history react-router-dom -S // Cài đặt 2 gói history và react-router-dom

```

Bây giwof ta cần kết nốt quá trình duyệt web với router và thằng Google analytics.

```ruby
import React from 'react';
import ReactDOM from 'react-dom';
import ReactGA from 'react-ga';
import { createBrowserHistory } from 'history';
import { Router } from 'react-router-dom';

const history = createBrowserHistory();

// Khởi tạo tới các page để tracking chúng
history.listen(location => {
  ReactGA.set({ page: location.pathname });
  ReactGA.pageview(location.pathname);
});

const App = () => (
  <Router history={history}>
    <AppComponent />
  </Router>
);

ReactDOM.render(<App />, document.getElementById('root'));

```


Vậy là bạn có thể thống kê việc tracking cho toàn bộ trang web của mình dựa vào google analytics.
[Branch tracking page view](https://github.com/khacthe/analytics_google_react/pull/3)


