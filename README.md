# docker-compose

---------------------
Create Network
---------------------

docker network create goals-net

---------------------
Run MongoDB Container
---------------------

docker run --name mongodb \
  -e MONGO_INITDB_ROOT_USERNAME=root \
  -e MONGO_INITDB_ROOT_PASSWORD=123456 \
  -v data:/data/db \
  --rm \
  -d \
  --network goals-net \
  mongo

---------------------
Build Node API Image
---------------------

docker build -t goals-node .

---------------------
Run Node API Container
---------------------

docker run --name goals-backend \
  -e MONGODB_USERNAME=root \
  -e MONGODB_PASSWORD=123456 \
  -v logs:/app/logs \
  -v E:/laragon/www/docker/docker-compose/backend:/app \
  -v /app/node_modules \
  --rm \
  -d \
  --network goals-net \
  -p 80:80 \
  goals-node

---------------------
Build React SPA Image
---------------------

docker build -t goals-react .

---------------------
Run React SPA Container
---------------------

docker run --name goals-frontend \
  -v E:/laragon/www/docker/docker-compose/frontend/src:/app/src \
  --rm \
  -d \
  -p 3000:3000 \
  -it \
  goals-react

---------------------
Stop all Containers
---------------------

docker stop mongodb goals-backend goals-frontend
