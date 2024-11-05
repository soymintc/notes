# SLURM
Personal cheatsheet

## Info about all partitions (nodes)
```bash
scontrol show node
```
or,
```bash
sinfo --Node --long
```

## Check cause of OOM kill
Example:
```bash
job_id=1837296
sacct -j $job_id --format=JobID,JobName,Partition,Account,AllocCPUs,State,ExitCode,Elapsed,TimeLimit,ReqMem,ReqCPUS
```
Will get something like:
```
JobID           JobName  Partition    Account  AllocCPUS      State ExitCode    Elapsed  Timelimit     ReqMem  ReqCPUS
------------ ---------- ---------- ---------- ---------- ---------- -------- ---------- ---------- ---------- --------
1838461      deepvaria+ componc_g+     shahs3          4    TIMEOUT      0:0   02:00:15   02:00:00     24000M        4
```

## Check CPU usage on cluster
```
sinfo -p componc_cpu -o "%C"
```
Will get something like:
```
CPUS(A/I/O/T)
1929/199/0/2128
```
Where `A`: Allocated, `I`: Idle, `O`: Other, `T`: Total

## One-liner submission
```bash
sbatch --partition=componc_cpu --job-name=test_job --output=output.txt --ntasks=1 --time=00:00:15 --mem=10MB --wrap="sleep 10"
```
