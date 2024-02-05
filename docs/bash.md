# Bash
Personal cheatsheet

## `sed` stdout vs file
```bash
cat some_file.txt | sed 's/pat1/pat2/g' # stdout
sed -i 's/pat1/pat2/g' some_file_to_overwrite.txt # file
```

## Check permissions recursively
```bash
namei -l /path/to/file
```

## Customize bjobs display
```bash
# WHAT-TO-DISPLAY:NUMBER_OF_CHRACTERS
bjobs -o "JOBID:10 SUBMIT_TIME:13 USER:5 STAT:5 QUEUE:6 EXEC_HOST:20 JOB_NAME"
```

## User-specific cache location
```bash
echo $XDG_CACHE_HOME  # you can set and export this in ~/.profile
                      # snakemake also looks for this cache directory
```
