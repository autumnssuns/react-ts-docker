# Keeptrack
My first TypeScript project, following the [Hands on React](https://handsonreact.com/docs/) tutorial.

## Installation

Start by cloning this repository:

```
git clone https://github.com/autumnssuns/react-ts-docker.git
```

### Docker
_Prerequisite: Docker must be running before attempting to run the application using this method. It is  recommended that Docker Desktop is used, as there will be need for the Docker Compose plugin._

Once Docker is running, deploy the application using:

```
docker-compose up -d
```

The following message should appear:

```
Starting react-ts_keeptrack_1 ... done
```

After this point, the application can be accessed at [http://localhost:3000/](http://localhost:3000/)

### Node Package Manager

_Prerequisite: `Nodejs` and Node Package Manager (`npm`) are required._

Navigate to `.\keeptrack` and run

```
npm install
npm start
```