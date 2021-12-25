## 1. Standard Approach

Sudo-code that should like an intro demo of data-fetching hooks: React-Query, SWR, etc.

```tsx
import {useQuery} from "your-library"

function Demo1() {
  const fetchTodos = useQuery(api.fetchTodos)

  if (fetchTodos.isLoading) {
    return <Loading/>
  }

  if (fetchTodos.error) {
    return <Message error={fetchTodos.error}/>
  }

  const data = fetchTodos.data! // *

  return <>
    {fetchTodos.data.map(todo =>
      <Todo todo={todo}/>
    )}
  </>
}
```

### Benefits & Drawbacks

Of the above code structure...

➕ Easy to write and to read<br/>
➕ Good enough in many cases<br/>
➖ Refetching may cause the component to reset to the `loading` state (depending on implementation)<br/>
➖ An `error` has a higher render priority than `data`<br/>
➖ A hint to the TS compiler that the data is defined is sometimes necessary at `*` line<br/>
