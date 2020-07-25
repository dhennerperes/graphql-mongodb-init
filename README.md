# graphql-mongodb-init

### commands docker
```
docker run \
    --name graphql-mongodb \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=dhenner \
    -e MONGO_INITDB_ROOT_PASSWORD=dhenner \
    -d \
    mongo:4

docker run \
    --name graphql-mongoclient \
    -p 3000:3000 \
    --link graphql-mongodb:graphql-mongodb \
    -d \
    mongoclient/mongoclient

docker exec -it graphql-mongodb \
    mongo --host localhost -u dhenner -p dhenner --authenticationDatabase dhenner
```

### commands graphql
```
mutation {
  addAuthor(name:"Author1", age:23){
    id
    name
    age
  }
}

mutation {
  addBook(name:"Book1", pages:230 ,authorID:"5f1c42f0b4d4133bdfb68880"){
    id
    name
    pages
  }
}

{
    book(id:"5f1c4384b4d4133bdfb68881"){
        id
        name
        pages
        author{
        id
        name
        age
        }
    }
}

{
	books{
    id
    name
    pages
    author{
      id
      name
      age
    }
  }
}

{
	authors{
        id
        name
        age
        book{
        id
        name
        pages
        }
    }
}

db.createUser(
{
    user: "dhenner",
    pwd: "dhenner",
    roles:[{role: "userAdmin" , db:"dhenner"}]
})

db.updateUser("dhenner", {
    roles: [
        { role: "dbAdmin", db: "dhenner" },
        { role: "readWrite", db: "dhenner" }
    ]
})
```