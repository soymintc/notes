# Bash
Personal cheatsheet

## `sed` stdout vs file
```bash
cat some_file.txt | sed 's/pat1/pat2/g' # stdout
sed -i 's/pat1/pat2/g' some_file_to_overwrite.txt # file
```
