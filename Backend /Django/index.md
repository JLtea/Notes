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
