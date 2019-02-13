# Exercises Day1

Install Hasura Console on local environment

### Prerequisites

For running GraphQL Api locally [Install Docker](https://docs.docker.com/install/)

then run `./run-hasura-locally.sh`

This will bring up docker container with Hasura engine with connection to existing Postgres API
You can read more about Hasura [here](https://medium.com/open-graphql/effortless-real-time-graphql-api-with-serverless-business-logic-running-in-any-cloud-8585e4ed6fa3)

Access Hasura console on localhost:8080/console

If you want to play around with your local version of postgres check this docs [link](https://docs.hasura.io/1.0/graphql/manual/getting-started/docker-simple.html)

- starwars api

[GraphiQL](https://graphql-bootcamp-swapi.herokuapp.com)

> Bonus you can add swapi custom server as remote schema in hasura console

[Remote schemas docs](https://docs.hasura.io/1.0/graphql/manual/remote-schemas/index.html#step-2-merge-remote-schema)

# Core principles

# Syntax and query language

Questions:

1. What's wrong with this syntax?

```
query {
  posts: {
    timestamp,
    users: {
      firstName
    }
  }
}
```

2. How to execute graphql request as curl

Answers:

1. The syntax shouldn't include colons (`:`) or commas (`,`) unless (generally) used in an argument. Also, `posts` doesn't contain a field `users` but does contain the field `user`.

```
query {
  posts {
    timestamp
    user {
      firstName
    }
  }
}
```

2. The above query as a `curl` command would look like:

```
curl -X POST -H "Content-Type: application/json" --data '{"query": "{ posts { timestamp user { firstName } } }"}' http://localhost:8080/v1alpha1/graphql
```

# Queries

Questions:

3. Get first 5 planets in Star Wars universe along with their name, diameter, rotation period, residents. For each resident display it's name, species, classification and spoken language. Also for each resident display vehicles that he used as well as in which movies they appeared

4) Get `subject` and `content` of `posts` ordered by `timestamp` ascending. Represent data as `ordered_posts` array

Answers:

3.

```
{
  allPlanets(first: 5) {
    planets {
      name
      diameter
      rotationPeriod
      residentConnection {
        residents {
          name
          species {
            name
            classification
            language
          }
          vehicleConnection {
            vehicles {
              name
              filmConnection{
                films {
                  title
                }
              }
            }
          }
        }
      }
    }
  }
}
```

4.

```
{
  ordered_posts: posts(order_by: { timestamp: asc }) {
		subject
    content
  }
}
```

# Mutations

Questions:

5. Add new blog post
6. Add a new user using GraphQL Mutation
7. Create reusable insert mutation called addPost, which not only will insert a post, but create new user and profile

   > Hint: use variables

Answers:

5. 6.

```
mutation addProfile {
  insert_profile(objects: [{
    bio: "GraphQL bootcamper, Vue.js fan"
  }]) {
    returning {
      id
    }
  }
}

mutation addUser {
  insert_users(objects: [{
  	firstName: "Alex"
    lastName: "Flasch"
    profileId: "cd24af27-efc1-41a8-9d43-40ee039bb43a"
  }]) {
    returning {
      id
    }
  }
}

mutation addPost {
  insert_posts(objects: [{
    subject: "My First GraphQL Mutation"
    content: "Hey this GraphQL thing is pretty nifty."
    userId: "412968b4-7d3b-45e6-8890-f447b6d031fc"
  }]) {
    returning {
      id
    }
  }
}
```

7.

```

```

# Subscriptions

Return `n` most liked post where `n` can be provided from outside.
