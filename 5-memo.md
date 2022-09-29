# memo from react.

- memo() là 1 Higher Order Component hay HOC.
- Dùng để bọc Component.
- memo sẽ ghi nhớ lại các props của 1 component , và quyết định liệu có re=render lại component hay ko .
- Tránh bị render trong các tình huống ko cần thiết.

```



export default memo(App);
```

- memo nhận vào component, mỗi lần component cha thay đổi sẽ check xem component của nó có bị thay đổi gì ko 
- và quyết định việc re-render.
- memo sẽ dùng toán tử === để so sánh. 