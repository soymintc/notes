# Singularity (and Docker)
Personal cheatsheet

## Troubleshooting
### Manifest unknown
For:
```bash
FATAL:   Unable to handle docker://A/B uri: failed to get checksum for docker://uhrigs/arriba: Error reading manifest latest in docker.io/A/B: manifest unknown: manifest unknown
```
Do:
```bash
singularity run docker://A/B:tag  # :tag will resolve issue
```

### Pull rate limit
For:
```bash
 => ERROR [internal] load metadata for docker.io/library/python:3.9                                                                                                                    2.9s
 ------
  > [internal] load metadata for docker.io/library/python:3.9:
  ------
  error: failed to solve: rpc error: code = Unknown desc = failed to solve with frontend dockerfile.v0: failed to create LLB definition: failed to copy: httpReadSeeker: failed open: unexpected status code https://registry-1.docker.io/v2/library/python/manifests/sha256:940ea29f268668b00305e22a93e3cbd0f3b05a221716a134f55a3ad8f88bc09f: 429 Too Many Requests - Server message: toomanyrequests: You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limit

```
Do:
```bash
docker login
```

### Resolving environmental variable collision
Since singularity inherits `env` variables by default while docker does not, some docker containers that depend on its own environment variables can show weird behaviors when run with singularity. Below is an example:
```bash
Illegal option --

Usage: /usr/bin/which [-a] args
```
Such collision can be resolved by putting in `--cleanenv` after either `singularity exec` or `singularity run`.
