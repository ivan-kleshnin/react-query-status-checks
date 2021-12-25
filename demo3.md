## 3. Alternative Approach

The repo author's preferred version.

```tsx
import {useQuery} from "your-library"

function Demo3Controller() {
  const fetchTodos = useQuery(api.fetchTodos)

  return <>
    {fetchTodos.error &&
      <Message error={fetchTodos.error}/>
    }}

    {fetchTodos.isLoading
      ? <Loading/>
      : <Demo3 data={fetchTodos.data} isFetching={fetchTodos.isFetching}/>
    }
  </>
}

type Demo3Props = {
  data : Data | undefined
  isFetching : boolean
}

function Demo3({data, isFetching} : Demo3Props) {
  if (!data || !data.someRequiredProp) {
    return <></>
  }

  return <>
    {isFetching && ...}
    {data.map(todo =>
      <Todo todo={todo}/>
    )}
  </>
}
```

### Benefits & Drawbacks

Of the above code structure...

➕ Easy to write and to read<br/>
➕ Good enough in most cases<br/>
➖ ~Refetching may cause the component to reset to the `loading` state~<br/>
➖ ~An `error` has a higher render priority than `data`~<br/>
➖ ~A hint to the TS compiler that the data is defined is sometimes necessary at `*` line~<br/>
➖ ~Errors are silenced as soon as there's any data~<br/>

### Extra Points

* Possible to add `isFetching` checks if necessary (all other versions also support it!)
* Possible to hide an error until the N-th refetch is tried (check `retryDelay` in R-Q)
* Code structure can be reused for actions/mutations as well!

### Test Cases

#### 1. Case: Query Disabled -> No data

1. UI: Should render Idle state (= typically nothing)

#### 2. Case: Loading -> Error

1. UI: Should render Loading
2. UI: Should render Error

#### 3. Case: Loading -> Data (Success)

1. UI: Should render Loading
2. UI: Should render Data

#### 4. Case: Loading -> Data -> Refocus -> Error (1st request) -> Data (2nd request)

1. UI: Should render Loading
2. UI: Should render Data
3. UI: Refocus
4. UI: Should render Error + Data
5. UI: Success (2nd attempt): should render Data



