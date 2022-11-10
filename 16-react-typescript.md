# Khai báo

- Function ;

  - let funcName : Function hoặc let funcName : (name: string) => void;

# định nghĩa kiểu dữ liệu với type :

```

type X = {
  a : string,
  b : number
}

type Y = X & {
  c : string,
  d : number
}

let y : Y = {
  c : 'aaa',
  d : 42,
  a : 'adsf',
  b : 12
}



```

# Định nghĩa kiểu dữ liệu với interface.

```

interface Person {
  name : string;
  age?: number;
}

interface Guy extends Person {
  profession: string;
}



```

# Khai báo React function

```

const App : React.FC = () => <div></div>;

const [todo, setTodo] = useState<string>('');
const [todo, setTodo] = useState<string | number[]>('');

```

- Khai báo type với props

```

interface Props {
  todo: string;
  setTodo: React.Dispatch<React.SetStateAction<string>>;
}

const NameCo = ({todo, setTodo} : Props) => <div></div>;
// or
const NameCo : React.FC<Props> = ({todo, setTodo}) => <div></div>;


```

- Hàm có sử dụng event :

```

const handleAdd = (e: React.FormEvent) => {
  e.preventDefault();
}

const inputRef = useRef<HTMLInputElement>(null);

```
