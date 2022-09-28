# useState có thể hiểu là trạng thái của dữ liệu.
- Dữ liệu thay đổi thì giao diện thay đổi. render lại giao diện.
-

# Cách dùng.

``` jsx 
import { useState } from 'react';

function Component() {
    const [state, setState] = useState(initState);

    ....
}

``` 

# Lưu ý.

- Component được re-render sau khi `setState`.
- Initial State sẽ chỉ được dùng cho lần đầu.
- Set state với callback ?



```
    setCounter(counter + 1); 
    setCounter(counter + 1); 
    setCounter(counter + 1); 

```

Sẽ chỉ chạy 1 lần , là counter ko thay đổi

sẽ khác với 

Bên dưới callback sẽ trả về giá trị mới cho state mỗi lần callback trả về


```
    setCounter(prevState => prevState + 1); 
    setCounter(prevState => prevState + 1); 
    setCounter(prevState => prevState + 1); 

```
- Cả 2 trường hợp trên react đều sẽ gộp lại và chỉ render 1 lần.
- Initial State với callback?

+ Khi truyền hàm vào initial State thì nó sẽ không dùng hàm làm giá trị khởi tạo. mà nó sẽ dùng value trước trả về từ 
+ callback để làm value khởi tạo.

- Set state là thay thế state với giá trị mới.

- Nếu ta setState bằng 1 object mới thì nó sẽ thay thế initial object cũ chứ ko phải là kiểu update.

- Ta có thể dùng callback trong setState.