# useEffect

- Được sử dụng với các side effect : Update DOM, Call API, Listen DOM events (scroll, resize), Clean up (remove listener, unsubscribe, Clear Timer)

- useEffect(callback, [deps])
- callback là hàm chạy
- deps là option và là 1 mảng

- callback sẽ luôn được gọi sau khi component được mounted

# useEffect(callback)

- Call back sẽ được gọi mỗi khi component được re-render.
- Gọi callback sau khi component thêm element vào trong DOM. tức là return được chạy xong. nhưng code vẫn chạy từ trên xuống.
- Tức là vẫn sẽ chạy useEffect nhưng ko chạy callback ngay.

# useEffect(callback, [])

- Chỉ gọi callback 1 lần sau khi component được mounted.

# useEffect(callback, [deps])

- deps là 1 biến .
- Callback sẽ được gọi là mỗi khi deps thay đổi.
- Callback vãn sẽ gọi mỗi khi được mounted
- Việc so sánh là dùng ===

# Clean up function.

- Clean up function , trong callback của useEffect ta có thể return về 1 hàm .
- Hàm được return về được gọi là clean up function.
- `clean up function sẽ được gọi trước khi component được unmounted.`
- `Clean up function sẽ luôn được gọi trước khi callback được gọi trừ lần đầu mounted`;
- trường hợp gọi trước callback là khi thay đổi state và useEffect được gọi là thì cleanup sẽ được gọi trước khi render và gọi lại useEffect. Tức là dọn dẹp lần trước đó r mới useEffect lần tiép theo.

```

useEffect(() => {
  window.addEventListerner('scroll', handleScroll);

  <!-- clean up functrion -->
  return () => {
    window.removeEventListerner('scroll', handleScroll);
  }

}, [])

```

## Khi dùng với setInterval

```

useEffect(() => {
    setInterval(() => {
      setCountdown(countdown - 1);
    }, 1000)
  }, []);

```

hàm trên sẽ chỉ gặp lỗi clouser , hàm callback sẽ chỉ chạy 1 lần nên sẽ luôn tham chiếu đến giá trị countdown cũ.

- Ta có thể dùng hàm callback với setCoundown.

```

useEffect(() => {
    setTimeout(() => {
      setCountdown(countdown - 1);
    }, 1000)
  }, [countdown]);

```

SetTimeout thì sẽ hoaạt động bth.

### Clean up image

```

const [avatar, setAvatar] = useState();

  useEffect(() => {

    return () => {
      avatar && URL.revokeObjectURL(avatar.preview);
    }

  }, [avatar]);

  const handlePreviewAvarta = (e) => {
    const file = e.target.files[0];


    file.preview = URL.createObjectURL(file);

    setAvatar(file);

  };

  return (
    <div>
      <input type="file" onChange={handlePreviewAvarta} />

      {
        avatar && <img src={avatar.preview} alt="" width='80%' />
      }
    </div>
  );

```
