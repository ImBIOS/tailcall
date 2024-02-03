# test-grpc-group-by

###### sdl error

#### server:

```graphql
schema @server(port: 8000, graphiql: true) @upstream(httpCache: true, batch: {delay: 10}) {
  query: Query
}

type Query {
  newsById(news: NewsInput!): News!
    @grpc(
      service: "news.NewsService"
      method: "GetMultipleNews"
      baseURL: "http://localhost:50051"
      body: "{{args.news}}"
      protoPath: "src/grpc/tests/news.proto"
      groupBy: ["id"]
    )
}
input NewsInput {
  id: Int
  title: String
  body: String
  postImage: String
}
type NewsData {
  news: [News]!
}

type News {
  id: Int
  title: String
  body: String
  postImage: String
}
```