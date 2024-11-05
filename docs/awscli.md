# AWS CLI
Personal cheatsheet

## Download aws s3 data with an access key and a secret key
```
export AWS_ACCESS_KEY_ID=SOMEAWSACCESSKEY
export AWS_SECRET_ACCESS_KEY=Some00Aws00Access0KeyF00Bar
aws s3 cp s3://path/to/s3/file.suffix /path/to/download
```

## Using `boto3` to download s3 objects
```python
s3 = boto3.client('s3', endpoint_url='https://gdc-jamboree-objstore.datacommons.io')
bucket_name = 'HCMI-CMDC-awg-lite' # sth like a root dir
local_directory = '../data/wgs/bam'  # dir to save files
s3_key = '9999999-9999-4999-9999-4999999999/52519999-9999-9999-9999-999999999_wgs_gdc_realn.bai'
try:
    s3.download_file(bucket_name, s3_key, local_path)
except Exception as e:
    print(f'Error downloading {s3_key}: {e}')
```
