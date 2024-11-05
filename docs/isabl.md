# Isabl
Personal cheatsheet<br>

Snippets below assumes:
    - you have `isabl_cli` is installed, and 
    - have imported it by `import isabl_cli as ii`

## Get analyses by filtering
1. Use case
```python
analyses = ii.get_analyses(
    application__name='ONT-DEEPSOMATIC',
    status='STARTED',
    targets__projects__pk=46,
    pk__gte=43753,
)
```

## Process `analysis` objects
1. Use case
```python
for analysis in analyses:
    print(analysis.pk)
    print(f"isabl apps-grch37 ont-deepsomatic-0.0.1 -p {analysis.targets[0].system_id} {analysis.references[0].system_id} --force")
```
