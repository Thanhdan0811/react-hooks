# useLayoutEffect

- So sánh với useEffect :

## useEffect

- 1. Cập nhật lại state.
- 2. Cập nhật DOM (mutated).
- 3. Render lại UI.
- 4. Gọi Cleanup nếu deps thay đổi.
- 5. Gọi useEffect callback.

## useLayoutEffect.

- 1. Cập nhật lại state.
- 2. Cập nhật DOM (mutated).
- 3. Gọi cleanup nếu deps thay đổi (sync).
- 4. Gọi useLayoutEffect callback (sync).
- 5. Render lại UI.

- Ta thấy với useLayoutEffect thì nó sẽ đẻ việc render lại ở lần cuối cùng.

```
function Content() {

  const [count, setCount] = useState(0);

  useEffect(()=> {
    if(count > 3) setCount(0);
  }, [count]);

  const handleRun = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={handleRun}>Run</button>
    </div>
  );

}

```

- Nếu dùng useEffect thì lức count bằng 3 và ta click Run tiếp , theo trình tự useEffect thì nó sẽ render lại ở bước 3,
- sau đó lại chạy callback của useEffect và set lại về 0, giao diện sẽ bị nháy từ 4 về 0

- Nếu dùng useLayoutEffect thì khi count là 3 và click tiếp Run thì ở bước 3 sẽ ko phải là render mà là call cleanup sau đó là gọi callback useLayoutEffect.
- Nên với useLayoutEffect sẽ ko có hiện số 4 mà sẽ quay về 0.
