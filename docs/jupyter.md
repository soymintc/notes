# Jupyter
Personal cheatsheet

## Launch session on server and port it to local
### On the server
```bash
PORT_SERVER=9988
jupyter lab --no-browser --port=$PORT_SERVER --ip "*"
```
### On local
```bash
PORT_SERVER=9988
PORT_LOCAL=9988 # does not have to be the same
ssh -L $PORT_SERVER:localhost:$PORT_LOCAL <MY_ID>@<SERVER_ADDRESS>
```
