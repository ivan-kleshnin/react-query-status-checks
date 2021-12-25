## 2. Inverted Approach

A version proposed by TkDodo in his article.

```tsx
import {useQuery} from "your-library"

function Demo1() {
  const fetchTodos = useQuery(api.fetchTodos)

  if (fetchTodos.data) {
    return <>
      {fetchTodos.data.map(todo =>
        <Todo todo={todo}/>
      )}
    </>
  }

  if (fetchTodos.error) {
    return <Message error={fetchTodos.error}/>
  }

  return <Loading/>
}
```

### Benefits & Drawbacks

Of the above code structure...

➕ Easy to write and to read<br/>
➕ Good enough in many cases<br/>
➖ ~Refetching may cause the component to reset to the `loading` state~<br/>
➖ ~An `error` has a higher render priority than `data`~<br/>
➖ ~A hint to the TS compiler that the data is defined is sometimes necessary at `*` line~<br/>
➖ Errors are silenced as soon as there's any data (new!)<br/>
