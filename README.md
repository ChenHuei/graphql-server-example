# graphql-server-example

# arguments

```
query {
  user(name: "leo") {
    name
    age
    height(unit: FOOT)
  }
}
```

# variables

```
query ($name: String!) {
  user(name: $name) {
    id
    name
  },
}

{
  "name": "leo"
}
```

# fragment, operation name, aliases

```
query UserData($name1: String!, $name2: String!) {
  user1: user(name: $name1) {
    ...userData
  },
  user2: user(name: $name2) {
    ...userData
  }
}

fragment userData on User {
  name
  height
  weight
}
```

# mutation

```
mutation  {
  addPost(title: "4", content: "Here's my third post.") {
    author {
      name
    }
    title
    content
    likeGivers {
      name
    }
  }
}
```

# input object type

```
type Mutation {
  addPost(title: String!, content: String!): Post
}

```

vs

```
# Mutation
  input AddPostInput {
    title: String!
    content: String
  }

  type Mutation {
    addPost(post: AddPostInput): Post
  }
```


# query + directives
```
query ($includeFriends: Boolean!, $skipSensitiveData: Boolean!) {
  users {
    name
    age @skip(if: $skipSensitiveData)
    friends @include(if: $includeFriends) {
      name 
    }
  }
}

{
  "includeFriends": false,
  "skipSensitiveData": true
}
```

# interface

```
共享 field


query {
  animals {
    name
  }
  animal(name: "Chiken Litte") {
    name
    ... on Bird {
      wingSpanLength
    }
    ... on Monkey {
      armSpanLength
    }
  }
}
```

# union

```
{
  search(keyword: "Mar") {
    ... on Magazine {
      name
    }
    ... on Book {
      title
    }
  }
}
```