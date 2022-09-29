# useRef

- Luê các giá trị thông qua 1 tham chiều bên ngoài function Component.
- Mỗi làn render lại component thì hàm sẽ tạo scope mới và các biến được khai báo trong hàm sẽ được tạo mới lại , ko lưu giá trị cũ
- useRef sẽ khắc phục điều này.

- const ref = useRef(initial); nhận vào giá trị khởi tạo. sử dụng lần đâu khi component được mounted. re-render thì sẽ ko đc dùng lại.
- useRef sẽ trả về 1 cái object. có dạng : {current: 99}
- mún thay đổi ta chỉ cần : ref.current = newValue.

```

function Content() {
  const [count, setCount] = useState(60);
  // const ref = useRef(99);

  const timerId = useRef();
  const preCount = useRef();
  const h1Ref = useRef();

  useEffect(() => {
    preCount.current = count;
  }, [count]);

  useEffect(() => {
    console.loog(h1Ref);
  });

  const handleStart = () => {
    timerId.current = setInterval(() => {
      setCount((prevCount) => prevCount - 1);
    }, 1000);
  };

  const handleStop = () => {
    clearInterval(timerId.current);
  };

  console.log(count, preCount.current);

  return (
    <div style={{ padding: 20 }}>
      <h1 ref={h1Ref}>{count}</h1>
      <button onClick={handleStart}>Start</button>
      <button onClick={handleStop}>Stop</button>
    </div>
  );
}


```

- console.log(count, preCount.current); Cố gắng hiểu chỗ này. lần đầu chạy sẽ là pre sẽ là 60, khi render lại thì sẽ return trước mới chạy callback useEffect.
