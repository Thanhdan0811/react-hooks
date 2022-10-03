# useMemo()

- lưu ý : memo là 1 HOC dùng cho component, useMemo là 1 hook được dùng trong function component.
- useMemo được dùng để tránh thực hiện lại 1 logic nào đó không cần thiết.


```
const UseMemo = ({ }) => {
    
    const [name, setName] = useState('');
    const [price, setPrice] = useState('');
    const [products, setProducts] = useState([]);
    const nameRef = useRef();

    const handleSubmit = () => {
        setProducts([...products, { name, price: +price }]);
        setName('');
        setPrice('');
        nameRef.current.focus();
    };

    const total = useMemo(() => {
        const result = products.reduce((result, prod) => {
            console.log('re-calculate');
            return result + prod.price;
        }, 0);

        return result;
    }, [products]);

    return (
        <div style={{ padding: '10px 32px' }}>
            <input type="text"
                value={name}
                placeholder='Enter name....'
                onChange={e => setName(e.target.value)}
                ref={nameRef}
            />
            <br />
            <input type="text"
                value={price}
                placeholder='Enter price....'
                onChange={e => setPrice(e.target.value)}
            />
            <br />
            <button onClick={handleSubmit}> Add </button>
            <br />
            Total: {total}
            <ul>
                {
                    products.map((product, idx) => {
                        return <li key={idx}>
                            {product.name} -
                            {product.price}
                        </li>
                    })
                }
            </ul>
        </div>
    );

};

```


- Khi dùng với memo thì useMemo và useCallback sẽ dùng khá giống nhau.