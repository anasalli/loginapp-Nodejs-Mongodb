//view this file in code view 
//i am using Rhel 9 and make sure 3000 port is open

git clone https://github.com/anasalli/loginapp-Nodejs-Mongodb.git
cd loginapp-Nodejs-Mongodb/loginapp
yum install nodejs npm -y

//install mongoDB (https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-red-hat/#std-label-install-mdb-community-redhat-centos)
vim /etc/yum.repos.d/mongodb-org-7.0.repo
[mongodb-org-7.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/7.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://pgp.mongodb.com/server-7.0.asc

yum install -y mongodb-org
systemctl enable --now mongod

//	Create a user with the necessary privileges on MongoDB
mongosh
use loginapp

//paste this
db.createUser({
  user: "myuser",
  pwd: "mypassword",
  roles: [{ role: "readWrite", db: "loginapp" }]
})

exit

//	Restart the MongoDB service
systemctl restart mongod


	 Start the Node.js Application:
node app.js



--> Verify Data on MongoDB database
mongosh
show dbs
use loginapp
db.users.find().pretty()   // here you can see you register users

