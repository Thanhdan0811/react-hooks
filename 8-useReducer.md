# useReducer

- Cung cấp thêm sự lựa chọn state cho function component.


- Các ví dụ :
- ví dụ 1 dơn giản :

```

import {   useReducer, useState } from "react";

// useState
// 1. Init State : 0
// 2. Actions : Up state + 1, Down state - 1;


// useReducer
// 1. Init State : 0
// 2. Actions : Up state + 1, Down state - 1;
// 3. Reducer
// 4. Dispatch
// Cần thêm 2 bước.

// Init state
const initState = 0;

// Actions
const UP_ACTION = 'up';
const DOWN_ACTION = 'down';

// Reducer (là 1 hàm)
// nhận vào state và action hiện tại trả về dữ liệu state mới dựa vào action.
// trả về đúng kiểu dữ liệu với init.

const reducer = (state, action) => {
    console.log('reducer running');
    switch (action) {
        case UP_ACTION:
            return state + 1;
        case DOWN_ACTION:
            return state - 1;
        default:
            throw new Error('Invalid  Action');
    }
}

/*
    dispatch sẽ là ussReducer, nhận vào tham số đầu tiên là reducer, 
    tham số thứ 2 là initState
    Khi Component lần đàu chạy thì sẽ chạy useReducer
    Ở lần đầu sẽ return về giá trị khởi tạo là 1 array.
    phần tử thứ 1 trong array là giá trị init, giá trị thứ 2 sẽ là 1 hàm.
    hàm này được gọi là dispatch
*/ 

const UseReducerCom = () => {
    // const [count, setCount] = useState(0);
    const [count, dispatch] = useReducer(reducer, initState);


    return (

        <div style={{ padding: '0 20px' }}>
            <h1>{count}</h1>
            <button
                // onClick={() => setCount(count - 1)}
                onClick={() => dispatch(DOWN_ACTION)}
            >
                Down
            </button>
            <button
                // onClick={() => setCount(count + 1)}
                onClick={() => dispatch(UP_ACTION)}
            >
                Up
            </button>
        </div>

    );
}

export default UseReducerCom;

```

- Ví dụ 2 : to do list

```



// useReducer

import { useReducer, useRef } from "react";

// 1. Init state
const initState = {
    job: '',
    jobs: []
};

// 2. actions
const SET_JOB = 'set_job';
const ADD_JOB = 'add_job';
const DELETE_JOB = 'delete_job';

const setJob = (payload) => {
    return { type: SET_JOB, payload };
};

const addJob = (payload) => {
    return { type: ADD_JOB, payload };
};

const deleteJob = (payload) => {
    return { type: DELETE_JOB, payload };
};

// 3. reducer
const reducerJob = (state, action) => {

    const { type, payload } = action;
    // console.log(type, payload);

    let newState; 

    switch (type) {
        case SET_JOB:
            newState = {
                ...state,
                job: payload
            };
            break;
        case ADD_JOB:
            newState = {
                ...state,
                jobs: [...state.jobs, payload]
            }
            break;
        case DELETE_JOB:
            
            newState = {
                ...state,
                jobs: state.jobs.filter((job, idx) => idx != payload)
            }
            break;
        default:
            throw new Error('Invalid action');
    };

    return newState;

};


const TodoListReducer = () => {

    const [state, dispatch] = useReducer(reducerJob, initState);
    const inputRef = useRef();

    const { job, jobs } = state;

    const handleSubmit = () => {
        dispatch(addJob(job));
        dispatch(setJob(''));
        inputRef.current.focus();
    }
    return (
        <div style={{padding: '0 20px'}}>
            <h3>To do</h3>
            <input 
                value={job} 
                type="text" 
                placeholder="Enter todo..." 
                onChange={(e) => {
                    dispatch(setJob(e.target.value));
                }}
                ref={inputRef}
            />
            <button
                onClick={handleSubmit}
            >
                Add                
            </button>
            <ul>
                {
                    jobs.map((jb, idx) => {
                        return <li key={idx}>{jb}
                            <span onClick={() => dispatch(deleteJob(idx))}>&times;</span>
                        </li>
                    } )
                }
            </ul>
        </div>
    );

}

export default TodoListReducer;


```

- Ta có thể chia ra các file : actions.js, reducer.js, setAction.js;