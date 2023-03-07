# Getting Started
QBCore is a framework created for FiveM RolePlay servers. QBCore can be deployed easily with the [txAdmin](https://txadm.in/) web panel, either locally on your computer or on your remotely hosted game server.

You will need to setup and start your database server first.

## Database
When deploying your QBCore server, you must ensure you have a database server running that can be accessed by the FiveM game server.

If you are using a VPS or creating a locally hosted server you can do this easily with [MariaDB Server](https://mariadb.org/en/#entry-header). MariaDB server is recommended due to its ease of use. It can be installed [here](https://native-network.net/downloads/download/895/).

!!! info "MariaDB Server"
    MariaDB Server is a general purpose open source relational database management system. This is a program that runs in the background of your game server and allows the FiveM server to store data.

    To view the database, you will need a database client, such as [HeidiSQL](https://www.heidisql.com/)

Some game server hosts will automatically setup your database and you will need to navigate the relevant control panel to access the database and will usually use **phpmyadmin**.

!!! tip "Zap-Hosting Guides"
    Zap-hosting has a tutorial [here](https://zap-hosting.com/guides/docs/en/gameserver_databases_pma/) for further reading.

## Installation