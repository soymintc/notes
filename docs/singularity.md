# Singularity (and Docker)
Personal cheatsheet

## Troubleshooting
For:
```bash
FATAL:   Unable to handle docker://A/B uri: failed to get checksum for docker://uhrigs/arriba: Error reading manifest latest in docker.io/A/B: manifest unknown: manifest unknown
```
Do:
```bash
singularity run docker://A/B:tag  # :tag will resolve issue
```
