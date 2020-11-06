# React js Notes

useState Hook with Objects

```
const [projects, setProjects] = useState({
    all: [],
    current: []
});
const {all, current} = projects;

/* setting initial state */
setProjects({
    all: data,
    current: currentData
});

/* when updating */
setProjects({
    ...projects,
    current: newdata // will replace 'current' and keep 'all'
});
```
