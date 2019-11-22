## How to create dump

### Go inside any running postgres docker

#### Run either of two from / (cd /)

```
pg_dump -U postgres  --no-acl  --no-owner  postgres > /raw_dump_acl.sql
pg_dump -U postgres postgres > /raw_dump.sql
```
