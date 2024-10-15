# Postgres docker-compose template

```yaml
# Use postgres/example user/password credentials
version: "3.9"

services:
  db:
    image: postgres:16.4-bullseye
    restart: always
    # set shared memory limit when using docker-compose
    shm_size: 128mb
    volumes:
      - ./data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: example
      POSTGRES_USER: user
      POSTGRES_DB: db_name
    ports:
      - "5432:5432"
```
