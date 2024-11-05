# Snakemake
Personal cheatsheet

## Arguments for lambda within a directive
```python
lambda wildcards, input, output, threads, resources: some_func(wildcards)
```

## Printing out simplified DAG
Instead of printing out all the wildcards when creating a DAG, you can use `--rulegraph` to only see the simplified DAG for all the rules:
```bash
snakemake \
... \
--rulegraph > pipeline.dag
```
And then maybe use `dot` for an SVG file:
```bash
cat pipeline.dag | dot -Tsvg > pipeline.svg
```
