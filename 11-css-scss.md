# dùng các import file css vào jsx

- Khi ta import file css vào jsx và chạy ở development thì nó sẽ thêm css vào theo kiểu là thẻ style trong head internal.
- Còn khi ở môi trường production (npm build) thí css sẽ được thêm ở dạng external.

# CSS module

- Khi tạo file css đăt tên như sau : nameFile.module.css
- thì lúc này webpack sẽ nhận định file này là 1 module và sẽ trả về 1 objec.
- Khi import vào file jsx : import style from './nameFile.module.css'
- style sẽ là object chứa các class mà ta định nghĩa trong file nameFile.module.css ()
- và ta cót hể dùng trong compnent như sau : className={style.class1}
- Nhược điểm ko thể dùng tag name độc lập.

# Thư viện thêm class name module nhiều class

- Để thêm nhiều class với module ta sẽ làm như sau : className={`${style.class1} ${style.class2}`}
- classnames và clsx sẽ giúp cú pháp nhìn gọn hơn.
- npm i clsx

```
import clsx from 'clsx';

style={clsx(style.btn, style.btn1)};
style={clsx(style.btn, {
  [style.btn1] : true || false
})};

```
# Cài sass/scss
- npm i sass 

# Cài nomolize 
- npm i --save normalize.css