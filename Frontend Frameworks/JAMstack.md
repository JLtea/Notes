# JAM stack notes

JavaScript, API & Markup

Benefits:

- Faster performance
  Serve pre-built markup and assets over a CDN

- More secure
  No need to worry about server or database vulnerabilities

- Less expensive
  Hosting of static files are cheap or even free

- Better developer experience
  Front end developers can focus on the front end, without being tied to a monolithic architecture. This usually means quicker and more focused development

- Scalability
  If your product suddenly goes viral and has many active users, the CDN seamlessly compensates

### Workflow

Develop => Version Control => Automated build => Static assets => Atomic deploy => Pre-render & invalidate cache => Update CDN

### Static Site Generators

- Gatsby
- 11ty
- Next.js
- Hugo
- Jekyll
- Nuxt

## React Data Fetching

- React Query
- Rest Hooks
- SWR
- React Async

### SWR stale-while-revalidate

1. Returns data from cache (stale)
2. Sends fetch request
3. Comes with the up-to-date data (revalidate)

- **JAMstack oriented**
- Fast, lightweight, and reusable data fetching
- **Built-in cache and request deduplication**
- Real-time experience
- Transport and protocol agnostic
- TypeScript ready
- React Native

useSWR parameters:

- data: data for the given key resolved by the fetcher (undefined if not yet loaded)
- error: the error thrown by the fetcher
- isValidating: boolean representing whether there is a request or revalidation in progress
- mutate(data?, shouldRevalidate): a function to mutate the cached data

**React component fetching without SWR**

```
const todosEndpoint = "http://localhost:3001/todos";
const TodoApp = () => {
  const [todos, setTodos] = useState([]);
  useEffect(() => {
    const getData = async () => {
      const response = await fetch(todosEndpoint);
      const data = await response.json();
      setTodos(data);
    };
     getData();
  }, []);
...
```

**Fetching with SWR**

```
import useSWR from "swr";
const todosEndpoint = "http://localhost:3001/todos";
const getData = async () => {
  const response = await fetch(todosEndpoint);
  return await response.json();
};
const TodoApp = () => {
  const { data: todos } = useSWR(todosEndpoint, getData);
...
```

SWR with other libraries

```
// axios

import axios from 'axios'
const fetcher = url => axios.get(url).then(res => res.data)
function App () {
  const { data, error } = useSWR('/api/data', fetcher)
  // ...
}

// GraphQL
import { request } from 'graphql-request'
const fetcher = query => request('https://api.graph.cool/simple/v1/movies', query)
function App () {
  const { data, error } = useSWR(
    `{
      Movie(title: "Inception") {
        releaseDate
        actors {
          name
        }
      }
    }`,
    fetcher
  )
  // ...
}
```

Mutate Example

```
import useSWR from "swr";
const todosEndpoint = "http://localhost:3001/todos";
// API CALLS
const getTodo = async (id) => {
  const response = await fetch(`${todosEndpoint}/${id}`);
  return await response.json();
};
const updateTodo = async (id, todo) => {
  const response = await fetch(`${todosEndpoint}/${id}`, {
    method: "PUT",
    headers: {
      "Content-type": "application/json; charset=UTF-8",
    },
    body: JSON.stringify(todo),
  });
  return await response.json();
};
// COMPONENT
const TodoApp = () => {
  const todoId = 1;
  const key = `${todosEndpoint}/${todoId}`;

  //SWR HOOK
  const { data: todo, mutate } = useSWR(key, () =>
    getTodo(todoId)
  );
  const toggleCompleted = async () => {
    const newTodo = {
      ...todo,
      completed: !todo.completed,
    };
    await updateTodo(todoId, newTodo);
    mutate(newTodo);
  };
...
```
