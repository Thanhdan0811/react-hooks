# Clean up call api.

```
  useEffect(() => {
    const controller = new AbortController();

    setLoading(true);

    fetch(url, {signal: controller.signal})
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));

    return () => {
      controller.abort();
    }

  }, [url])


```

# Reference equality

```
const [age, setAge] = useState(0);
const [name, setName] = useState('');
const [darkMode, setDarkMode] = useState(false);



const person = { age: age, name: name };

useEffect(() => {
  console.log(person);
}, [person]);


```

- Khi ta thay đổi state darkMode thì cả person cũng sẽ bị thay đổi.
- Do mỗi lần ta re-render thì biến person sẽ được tạo mới do reference.
- Để khắc phực ta sẽ dùng useMemo

```

const [age, setAge] = useState(0);
const [name, setName] = useState('');
const [darkMode, setDarkMode] = useState(false);



const person = useMemo(()=> {
    return { age: age, name: name };
}, [age, name]);

useEffect(() => {
  console.log(person);
}, [person]);


```

- Sẽ chỉ trả về new object mỗi khi age hoặc name thay đổi.
- Chú ý với các dữ liểu kiểu khác như array....
