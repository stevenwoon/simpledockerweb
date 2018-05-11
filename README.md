cd $HOME/docker
sudo npm i -g express
express dummy-app
cd dummy-app
npm install
DEBUG=dummy-app:* npm start

Dockerfile
----------
FROM mhart/alpine-node:latest:wq
ADD package.json /tmp/package.json
RUN cd /tmp && npm install
RUN mkdir -p /opt/app && cp -a /tmp/node_modules /opt/app/

WORKDIR /opt/app
ADD . /opt/app

EXPOSE 3000

CMD ["npm", "start"]
---------

docker build -t dummy-app .


Test
curl -X POST -H "Content-type: application/json" http://localhost:3000/data/into/db -d '[ { "a": 1 }, { "b": 2 }, { "c": 3 } ]'

