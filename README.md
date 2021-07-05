<h1 align="center">Twitter API Clone in Rust</h1>

# Content
- [Requirements](#requirements)
- [Development](#development)
- [API](#api)
- [Support](#support)
- [License](#license)

### Requirements

- Rust on the stable channel
- PostgreSQL

### Development:

1. Clone this repository & open in terminal.
2. Set `DATABASE_URL` env varibale.

```sh
export DATABASE_URL=postgres://user:password@localhost/twitter
```
2. Configure database

```sh
diesel setup
diesel migration run
```

4. Run program

```sh
cargo run
```

5. Call API:

```sh
curl -X POST -d '{"message": "Hello world!"}' -H "Content-type: application/json" http://localhost:9090/tweets
```

## API

- Create (`POST`) a tweet

```sh
curl -X POST -d '{"message": "Hello world!"}' -H "Content-type: application/json" http://localhost:9090/tweets
```

returns:

```json
{
    "id": "584bca73-9d63-4801-bafc-ded7241a159f",
    "created_at": "2020-07-04T13:35:48.059039Z",
    "message": "Hello world",
    "likes": []
}
```

- `DELETE` a tweet with `id`:

```sh
curl -X DELETE http://localhost:9090/tweets/90c76a57-8d6f-46cb-b68a-ef7dc67fdc6e
```

Return status code: 204 in any case.

- `GET` all tweets:

```sh
curl http://localhost:9090/tweets
```

returns list of tweets:

```json
{
    "results": [{
        "id": "90c76a57-8d6f-46cb-b68a-ef7dc67fdc6e",
        "created_at": "2020-07-04T19:10:47.856376Z",
        "message": "Hello world!",
        "likes": []
    }, {
        "id": "584bca73-9d63-4801-bafc-ded7241a159f",
        "created_at": "2020-07-04T19:04:01.448201Z",
        "message": "Hey world!",
        "likes": []
    }]
}
```

- `GET` Tweet by `id`:

```sh
curl http://localhost:9090/tweets/90c76a57-8d6f-46cb-b68a-ef7dc67fdc6e
```

if tweet exists returns:

```json
{
    "id": "90c76a57-8d6f-46cb-b68a-ef7dc67fdc6e",
    "created_at": "2020-07-04T19:10:47.856376Z",
    "message": "Hello world!",
    "likes": [{
        "id": "08a5f40f-4639-4882-8e0d-84ff84621461",
        "created_at": "2020-07-04T19:22:29.095815Z"
    }]
}
```

otherwise it returns status code `204`.

- `GET` list of likes for tweet with `id`:

```sh
curl http://localhost:9090/tweets/90c76a57-8d6f-46cb-b68a-ef7dc67fdc6e/likes
```

return list of like for tweet with `id`:

```json
{
    "results": [{
        "id": "08a5f40f-4639-4882-8e0d-84ff84621461",
        "created_at": "2020-07-04T19:22:29.095815Z"
    }]
}
```

- ADD (`POST`) one like to a tweet:

```sh
curl -X POST http://localhost:9090/tweets/90c76a57-8d6f-46cb-b68a-ef7dc67fdc6e/likes
```

returns:

```json
{
    "id": "08a5f40f-4639-4882-8e0d-84ff84621461",
    "created_at": "2020-07-04T19:22:29.095815Z"
}
```

- `DELETE` one like to a tweet

```sh
curl -X DELETE http://localhost:9090/tweets/90c76a57-8d6f-46cb-b68a-ef7dc67fdc6e/likes
```

## Support

Post issues and feature requests on the GitHub [issue tracker](https://github.com/minikin/twitter-rs/issues).

## License

The source code of a project is available under the MIT license.
See the [LICENSE](https://github.com/minikin/twitter-rs/LICENSE) file for more info.
