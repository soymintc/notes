# TCGA
Personal cheatsheet - sick and tired of looking up how to login

## Wiki
1. Go directly to the wiki page
2. Login using MSK email using Google OAuth
3. If everything fails due to cookies, clear them and try again, or try Chrome incognito mode

## Synapse
1. Go to https://www.synapse.org 
2. Login using MSK email using Google OAuth

### downloading files
```
pip install synapseclient
synapse login # will ask for ID and password (can set in Accounts)
synapse get-download-list
```
