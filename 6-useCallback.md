# useCallback()

- Tránh tạo ra các hàm mới 1 cách không cần thiết trong function Component.

```
<!-- APP component -->

function App() {
    const [count, setCount] = useState(0);

    const handleIncrease = () => {
        setCount(preCount => preCount + 1);
    };

    return (
        <div>
            <Content onIncrease={handleIncrease} />
            <h1>{count}</h1>
        </div>
    );  
};

<!-- Content Component -->

function Content({onIncrease}) {
    console.log('re-render');

    return (
        <>
            <h2>Hello</h2>
            <button onClick={onIncrease}> Click me </button>
        </>
    )
};

export default memo(Content);


```

- Ở ví dụ trên mặc dù ta dúng memo với Content nhưng khi App component re-render thì Content component cũng re-render.
- Vì khi re-render App component thì hàm handleIncrease sẽ cập nhật tham chiều mới lúc đó props onIncrease cũng sẽ thay đổi.

# khắc phục với useCallback
- useCallback nhận vào 2 đối số : tham số đầu là hàm cần truyền vào, tham số thứ 2 là deps [] như useEffect

```

    const handleIncrease = useCallback( () => {
        setCount(preCount => preCount + 1);
    } , []);

```

- Ở lần đầu mounted , useCallback sẽ nhận vào hàm và lưu tham chiếu hàm ra bên ngoài scope của App component.
- Sau đó sẽ trả về lại tham chiếu đó.
- Khi App component re-render thì useCallback sẽ trả lại tham chiếu đó nếu có deps [].
- Nếu trong hàm có sử đụng state thì ta sẽ truyền state vào deps để mỗi khi state thay đổi sẽ tạo mới 1 tham chiếu cho hàm.

# NOTE 
- useCallback thường sẽ dùng mới memo trong react.
- vì nếu ko có memo thì khi component cha re-render thì component con cũng sẽ re-render theo.