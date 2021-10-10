# CHAT APP

Es una aplicacion de chat en tiempo real desarrollada con Angular como Frontend y NestJs para el Backend
El repositorio del Servidor se encuentra en este [link](https://github.com/ararcos/real-chat-server)
El repositorio del Cliente se encuentra en este [link](https://github.com/ararcos/real-chat-client)

La aplicacion se encuentra deployada en Vercel para el Frontend y Heroku para el Backend

#### Froentend
[https://real-chat-client.vercel.app/](https://real-chat-client.vercel.app/)

#### Backend
[https://chat-app-porth.herokuapp.com/](https://chat-app-porth.herokuapp.com/)

Contents
========
 * [Installation Backend](#installation-backend)
 * [Installation Frontend](#installation-frontend)
 * [Arquitecture](#arquitecture)
 * [Approach and Methodology](#approach-and-methodology)

## Installation Backend

Chat App Frontend requiere [Node.js](https://nodejs.org/) , [NestJs](https://nestjs.com/) y [Docker](https://www.docker.com/) para correr.

Clonar el proyecto:
```sh
git clone https://github.com/ararcos/real-chat-server
```

Instalar las dependencias 
```sh
cd real-chat-server
npm install
```
Crear el contenedor con PosgresSQL y correr las migrationes
```sh
cd real-chat-server
docker-compose up
npm run migration:run
```
Iniciar el Servidor.
Para iniciar toca cambiar la configuracion del archivo database.service.ts remplazando ssl:true a false como el ejemplo siguiente
```javascript
return {
        type: 'postgres' as const,
        ssl: true,
        extra: {
          ssl: {
            rejectUnauthorized: false,
          },
        },
        host: config.get(Configuration.DB_HOST),
        port: parseInt(config.get(Configuration.DB_PORT)),
        username: config.get(Configuration.DB_USER),
        password: config.get(Configuration.DB_PASS),
        database: config.get(Configuration.DB_NAME),
        entities: [__dirname + '/../**/*.entity{.ts,.js}'],
        migrations: [__dirname + '/migrations/*{.ts,.js}'],
      } as ConnectionOptions;
```
por una conecion sin ssl
```javascript
return {
        type: 'postgres' as const,
        ssl: false,
        host: config.get(Configuration.DB_HOST),
        port: parseInt(config.get(Configuration.DB_PORT)),
        username: config.get(Configuration.DB_USER),
        password: config.get(Configuration.DB_PASS),
        database: config.get(Configuration.DB_NAME),
        entities: [__dirname + '/../**/*.entity{.ts,.js}'],
        migrations: [__dirname + '/migrations/*{.ts,.js}'],
      } as ConnectionOptions;
```
Luego iniciamos el servidor
```sh
cd real-chat-server
npm run start
```

## Installation Frontend
Chat App Frontend requiere [Node.js](https://nodejs.org/) , [Angular](https://angular.io/)  para correr.

Clonar el proyecto:
```sh
git clone https://github.com/ararcos/real-chat-client
```

Instalar las dependencias y iniciar servidor
```sh
cd real-chat-client
npm install
ng serve
```
