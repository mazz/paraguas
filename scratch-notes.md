# phoenix generate prod assets

## paraguas/apps/phoenix_app/

cd assets && npm install babel-preset-latest && node node_modules/brunch/bin/brunch build

npm install


# prod build

## paraguas/apps/phoenix_app/assets 

npm install
./node_modules/brunch/bin/brunch b -p

## paraguas/apps/phoenix_app

MIX_ENV=prod mix phx.digest

## paraguas

MIX_ENV=prod mix release

## prod run, no params

./_build/prod/rel/paraguas/bin/paraguas foreground

## prod run, params

REPLACE_OS_VARS=true \
  PORT=4000 \
  COOKIE=cookie \
  SOMBRILLA=42 \
  _build/prod/rel/paraguas/bin/paraguas foreground

## sudo for port 80

sudo REPLACE_OS_VARS=true \
  PORT=80 \
  COOKIE=cookie \
  SOMBRILLA=42 \
  _build/prod/rel/paraguas/bin/paraguas foreground

## sudo for port 443

sudo REPLACE_OS_VARS=true \
  PORT=443 \
  COOKIE=cookie \
  SOMBRILLA=42 \
  _build/prod/rel/paraguas/bin/paraguas foreground

## blow-away docker images

docker rm -f $(docker ps -a -q)
docker rmi $(docker images -q)
docker system prune -a -f

## docker build

docker build -t paraguas:0.1.0 .

## docker run

docker run --rm -ti \
             -p 80:80 \
             -e COOKIE=a_cookie \
             -e SOMBRILLA=42 \
             paraguas:0.1.0

## docker ps && docker kill

docker ps
docker kill <image name>


## this didn't work:

mkdir -p ./_build/prod/lib/phoenix_app/priv/static/.well-known
(cd ./_build/prod/lib/phoenix_app/priv/static && \
 echo "hello world" > .well-known/XXXYYY.html)

## adding .well-known to /home/maz/src/paraguas-mazz/apps/phoenix_app/assets/static
 
then run ```MIX_ENV=prod mix phx.digest```

## install certbot

(apt-get install -y software-properties-common && \
 add-apt-repository -y ppa:certbot/certbot && \
 apt-get update && \
 apt-get install -y certbot)

## this works but you have to stop the webserver(port 80)

 certbot certonly --standalone -d maz.me -d www.maz.me
