# Django Notes

### Useful ORM tools

```
# filter
results = example.objects.filter(somefield__contains='tag', job_id=id).count()
# get values
results = example.objects.values('name', 'label', 'other')
# annotate
results = example.objects.values('type', 'name').annotate(count=Count('type'), name_count=Count('name'))
# select related
results = example.objects.select_related('label).values('label__name').annotate(Count('label_id'))

```

## Raw Queries

For Single Object

```
tasks = Task.objects.raw('SELECT id, size FROM engine_task WHERE project=%s',[project])
for task in tasks:
    # Do something
```

For more complex queries

```
from django.db import connection
def dictfetchall(cursor):
    "Return all rows from a cursor as a dict"
    columns = [col[0] for col in cursor.description]
    return [
        dict(zip(columns, row))
        for row in cursor.fetchall()
    ]
with connection.cursor() as cursor:
    cursor.execute('SELECT * FROM datatable ")
    data = dictfetchall(cursor)
```

Using Parameters:

```
cursor.execute('SELECT * FROM datatable WHERE id=%s', [id])

# Arrays need to be in tuple

cursor.execute('SELECT * FROM datatable WHERE id IN %s, [tuple(id_list)])
```
