# GraphQL Cheat Sheet
## Introduction
GraphQL (Graph Query Language) is an API query language that is designed to facilitate efficient communication between clients and servers.

Key Features:
- Declarative: Clients describe what data they need.
- Efficient: Reduces over-fetching and under-fetching compared to REST.
- Strongly typed: Uses a schema to define the structure of the API.
- Single endpoint: All queries go through one endpoint

Types of operations:
- Queries - fetch data.
- Mutations - modify data.
- Subscriptions - set up a permanent connection between client and server (websocket)


## Common GraphQL endpoints
```
/graphql
/api
/api/graphql
/graphql/api
/graphql/graphql
```

## Queries
`Fields` are the pieces of data user request.\
`Arguments` are inputs you provide to fields to customize or filter the data.\
`Variables` enable to pass dynamic arguments, rather than having arguments directly within the query itself.\
`Fragments` let you re-use parts your query to avoid repetition.


### Basic query
Request:
```
query {
  users {
    id
    name
    email
  }
}
```

Response:
```
{
  "data": {
    "users": [
      {
        "id": "1",
        "name": "Alice",
        "email": "alice@example.com"
      },
      {
        "id": "2",
        "name": "Bob",
        "email": "bob@example.com"
      }
    ]
  }
}
```

### Query with variable
Request:
```
query getUser($userid: ID!) {
  user(id: $userid) {
    id
    name
    email
  }
}

Variables:
{
  "userid": "1"
}
```

Response:
```
{
  "data": {
    "user": {
      "id": "1",
      "name": "Alice",
      "email": "alice.1@example.com"
    }
  }
}
```

### Filtered query
Request:
```
query {
  users(name: "Alice") {
    id
    name
    email
  }
}
```

Response:
```
{
  "data": {
    "users": [
      {
        "id": "1",
        "name": "Alice",
        "email": "alice.1@example.com"
      },
      {
        "id": "3",
        "name": "Alice",
        "email": "alice.2@example.com"
      }
    ]
  }
}
```

### Aliased query
Request
```
query getusers{
  user1: user(id: "1") {
    name
    email
  }
  user2: user(id: "2") {
    name
    email
  }
}
```

Response:
```
{
  "data": {
    "user1": {
      "name": "Alice",
      "email": "alice@example.com"
    },
    "user2": {
      "name": "Bob",
      "email": "bob@example.com"
    }
  }
}
```

### Fragments
Request:
```
fragment userFields on User {
  id
  name
  email
}

query {
  user(id: "1") {
    ...userFields
  }
  admin(id: "2") {
    ...userFields
  }
}
```

Response:
```
{
  "data": {
    "user": {
      "id": "1",
      "name": "Alice",
      "email": "alice.1@example.com"
    },
    "admin": {
      "id": "2",
      "name": "Bob",
      "email": "bob@example.com"
    }
  }
}
```

### Mutation
The `input` field in a GraphQL mutation is not always obligatory — it depends entirely on how the schema is defined by the backend.

Request:
```
mutation {
  createUser(input: { name: "Alice", email: "alice.1@example.com" }) {
    id
    name
    email
  }
}
```

Response:
```
{
  "data": {
    "createUser": {
      "id": "1",
      "name": "Alice",
      "email": "alice.1@example.com"
    }
  }
}
```

