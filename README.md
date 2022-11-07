[![Node.js CI](https://github.com/notrustverify/pastenym/actions/workflows/frontend.yml/badge.svg)](https://github.com/notrustverify/pastenym/actions/workflows/frontend.yml)

# pastenym

This project is inspired from [pastebin](https://pastebin.com/) service.
The main goal is to offer a solution for sharing text with [Nym](https://nymtech.net/) products
to offer full anonymity, even on metadata level

#### Demo
Get shared text: [http://pastenym.ch/zXruebin](http://pastenym.ch/zXruebin)

Share a text: [http://pastenym.ch/](http://pastenym.ch/)

## What Nym is developping ?
> Nym is developing the infrastructure to prevent this data leakage by protecting every packet’s metadata at the network and application layers.

### Architecture

<img src="./resources/img/nym-platform.png" alt="drawing" width="50%"/>

## How pastenym service will use Nym product
Your text is sent to a client which is connected to the Nym network and which stores it in a database (eventually a more distributed solution will be considered),



This system allows you to share information while respecting your privacy by protecting your data and metadata.

On the side of No Trust Verify we only see an anonymous id when sending the text, and therefore impossible to know who is behind and from where the data was sent.

### Schema

<img src="./resources/img/paste.jpg" alt="drawing" width="60%"/>

## Init the project

### Nym client
1. Download [nym-client](https://github.com/nymtech/nym/releases/tag/nym-binaries-1.0.2)
2. Give exec permissions and init the client
```bash
chmod u+x nym-client
./nym-client init --id pastenym --gateway EBT8jTD8o4tKng2NXrrcrzVhJiBnKpT1bJy5CMeArt2w
```
3. Run the client `./nym-client run --id pastenym`

### Backend
It uses [pipenv](https://pipenv.pypa.io/en/latest/install/)

1. Go to `backend/`
2. `pipenv shell` to start the python env
3. `pipenv install` to install the dependancies from the PipFile
4. `python -c "from db import *; create_tables()" ` to init the DB
5. `python main.py` to start the service

### Frontend
NodeJS and npm are used

* npm version `8.19.2`
* nodejs version `v16.13.1`

1. Go to `js-example/`
1. `npm install`
2. `npm run start` open the browser and go to [http://localhost:8081](http://localhost:8080)

### Docker

1. Download the [custom nym-client](https://nym.notrustverify.ch/resources/nym-client). It just a recompiled version that can listen to `0.0.0.0`
2. Init the nym-client and copy files 
```bash
cd nym-client
chmod u+x nym-client
./nym-client init --id docker-client --gateway EBT8jTD8o4tKng2NXrrcrzVhJiBnKpT1bJy5CMeArt2w
cp -r ~/.nym/clients/docker-client nym-data/clients
```

3. Change path in config.toml. For example with user root, search `/home/root` and replace by `/home/user`
4. `docker compose up --build -d`

## Structure

* `backend/` manage the websockets connections and DB
* `frontend/` web application
* `nym-client/` store the configuration,keys for the nym-client
* `resources/` store img or files for documentation
