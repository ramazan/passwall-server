# PassWall

![GitHub](https://img.shields.io/github/license/pass-wall/passwall-api)
![GitHub issues](https://img.shields.io/github/issues/pass-wall/passwall-api)
[![Build Status](https://travis-ci.org/pass-wall/passwall-api.svg?branch=master)](https://travis-ci.org/pass-wall/passwall-api) 
[![Coverage Status](https://coveralls.io/repos/github/pass-wall/passwall-api/badge.svg?branch=master)](https://coveralls.io/github/pass-wall/passwall-api?branch=master)

**PassWall** is an open source password manager API written with Go.

By using this API you can store your passwords wherever you want and manage easily event with just Postman etc.

## What's possible with PassWall API?

Currently, this project is focused on storing URL, username and password which is basically called **Login** at PassWall API.

An admin can;

- Sign in and Refresh token
- View all logins
- View a specific login
- Create login with automatically generated strong password
- Update login
- Delete login


## API Documentation
API documentation available at:   
[Click to see at Public Postman Templates](https://documenter.getpostman.com/view/3658426/SzYbyHXj)  

## Authentication

This API uses **JWT Token** to secure endpoints. So user must generate token with /auth/signin first. Then with generated token, all endpoints in API documentation can be reachable.  
  
User information for signin is in **config.yml** file.

## Development usage
Just change **config-sample.yml** to **config.yml** in **store** folder and update the content of this file for your usage. Then you can run API with standard command:

```
go run main.go
```

## docker-compose

You can start PassWall API with a database by one line command:

**P.S: You should uncomment database service sections**

```
docker-compose up --build
```

## Docker usage
First get into you project folder. Then:

To build
```
docker build -t passwall-api .
```

To run
```
cp ./store/config-sample.yml ./store/config.yml
docker run --name passwall-api --rm -v $(pwd)/store:/app/store -p 3625:3625 passwall-api
```

To store persistent data (config.yml and passwall.db)
```
mkdir $HOME/docker/volumes/passwall-api
cp ./store/config-sample.yml $HOME/docker/volumes/passwall-api/config.yml
docker run --name passwall-api -d --restart=always -v $HOME/docker/volumes/passwall-api:/app/store -p 3625:3625 passwall-api
```

## Import
There are different kinds of password managers. Almost all of them can export login information as CSV file. Here is an example CSV file (let's say example.csv).  
![example csv](https://www.yakuter.com/wp-content/yuklemeler/example-csv.png "Example CSV File")  
  
You need to fill the import form as below picture.  
![passwall-api import](https://www.yakuter.com/wp-content/yuklemeler/passwall-api-import-csv.png "Import Form and Request Example")
