# xielaoban
xielaoban,e-commerce


# mongodb on ubuntu16.04lts

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list

(ubuntu14.04)
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list

sudo apt-get update

sudo apt-get install -y mongodb-org


# redis

sudo apt-get update
sudo apt-get install redis-server

# start service
mongod &              # start mongodb
redis-server &        # start redis
rabbitmq-server &     # start RabbitMQ

# Initial database

python3 manage.py shell
# into Python3 shell
>>> from application.models import User
>>> user = User.create(email="xxxx@xxx.com", password="xxx", name="xxxx")
# Rename the email, password, name
>>> user.roles.append("ADMIN")
>>> user.save()
Run server

# start celery
celery -A application.cel worker -l info &

python3 manage.py runserver
