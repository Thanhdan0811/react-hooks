# Add a Routing

```

    <Router>
        <Routes>
            <Route path='/' element={<App />}>
                <Route path='expenses' element={<Expenses/>} />
                <Route path='invoices' element={<Invoices />}>
                    <Route
                        index
                        style={{padding: "1rem"}}
                        element={
                            <main>
                                <p>Select an Invoice</p>
                            </main>
                        }
                    />
                    <Route path=':invoiceId' element={<Invoice/>} />
                </Route>
                <Route path='*' element={
                    <main style={{padding: '1rem'}}>
                        <h1>Page not found!!!</h1>
                    </main>
                } />
            </Route>
        </Routes>
    </Router>

```

## Index Route

- index route sẽ chia sẻ chung path với path của parent.
- Do đó index ko có path.

- Index route render trong parent routes outlet tại parent route's path (tại path route của parent).
- Index route sẽ match khi 1 parent route matches nhưng không có bất cứ children route nào match.
- Index route là là default child route của 1 parent route.
- Index route render khi mà user chưa click vào bất cứ item nào trong navigation list.

# Link to NavLink để hiện active LInk.


```

<NavLink
    style={({ isActive }) => {
        return {
        display: "block",
        margin: "1rem 0",
        color: isActive ? "red" : "",
        };
    }}
    to={'/invoices/' + invoice.number}
    key={invoice.number}
>
  {invoice.name}
</NavLink>

<NavLink className={({ isActive }) => isActive ? "red" : "blue"} />

```


- Ta đổi style từ object thành function return về 1 object.
- biến isActive ssẽ được pass từ style funciton.
- Có thể áp dụng cho className.


## Search params sau dấu ?
- React router sử dụng useSearchParams để lấy và thao tác params.
- useSearchParams hoạt động giống với useState.
- Chỉ khác là lưu và set state trong URL search params thay vì trong memory.


```
let [searchParams, setSearchParams] = useSearchParams();

value={searchParams.get("filter") || ""}

```

- searchParams sẽ có các method như get, set.....
- https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams : api của URLSearchParams
- useSearchParams sẽ return về URLSearchParams với '"filter"' là 1 value của nó.
- Ta sẽ setSearchParams giống như với useState nhưng là trong URLSearchParams.


## Custom Behavior.
- Để vẫn giữ được url với "?filter=..." khi ta click vào NavLink thì sẽ dùng useLocation.

```

function QueryNavLink({ to, ...props }) {
  let location = useLocation();
  console.log(location);
  return <NavLink to={to + location.search} {...props} />;
}


{invoices
          .filter((invoice) => {
            let filter = searchParams.get("filter");
            if (!filter) return true;
            let name = invoice.name.toLowerCase();
            return name.startsWith(filter.toLowerCase());
          })
          .map((invoice) => (
            <QueryNavLink
              style={({ isActive }) => {
                return {
                  display: "block",
                  margin: "1rem 0",
                  color: isActive ? "red" : "",
                };
              }}
              to={"/invoices/" + invoice.number}
              key={invoice.number}
            >
              {invoice.name}
            </QueryNavLink>
          ))}

```

- Cách viết sẽ như HOC. 
- useLocation() sẽ trả về object có dạng như sau : 

```

{
  pathname: "/invoices",
  search: "?filter=sa",
  hash: "",
  state: null,
  key: "ae4cz2j"
}

```


- Ví dụ phức tạp hơn.

```

function BrandLink({ brand, ...props }) {
  let [params] = useSearchParams();
  let isActive = params.getAll("brand").includes(brand);
  if (!isActive) {
    params.append("brand", brand);
  } else {
    params = new URLSearchParams(
      Array.from(params).filter(
        ([key, value]) => key !== "brand" || value !== brand
      )
    );
  }
  return (
    <Link
      style={{ color: isActive ? "red" : "" }}
      to={`/shoes?${params.toString()}`}
      {...props}
    />
  );
}

```

- Ví dụ trên sẽ hiển thị các brand chưa có và sẽ remove brand đi nếu brand đó được chọn lại lần nữa.


