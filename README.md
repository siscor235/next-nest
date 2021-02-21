# NestJS Playground

## Usage

```sh
docker-compose up
docker-compose exec web npm run console -- seed
docker-compose exec web npm run lint
docker-compose exec db psql -U postgres -c 'create database test;'
docker-compose exec web npm run test
docker-compose exec web npm run test:e2e
```

http://localhost:3000/graphql

```graphql
query EmployeeSpendsByCompany($companyId: Int = 1, $month: DateTime = "2020-02-03") {
  employeesByCompany(companyId: $companyId) {
    id
    name
    spend
    spendInMonth(month: $month) {
      total
      taxFree
      taxable {
        thirtyPercentBracket
      }
    }
  }
}

query PartnerRevenues {
  partners {
    id
    name
    revenue
  }
}
```

### Useful commands

Nest CLI:
```
docker-compose exec web npm run nest -- --help
```

TypeORM CLI:
```
docker-compose exec web npm run typeorm -- --help
```

## Learnings

Resources:
- https://github.com/jmcdo29/testing-nestjs

Limitations:
- Nested queries not supported by TypeORM https://github.com/typeorm/typeorm/issues/2707#issuecomment-748011818
- No schema in TypeORM: https://github.com/typeorm/typeorm/issues/664
- No upsert in TypeORM: https://stackoverflow.com/questions/46745688/typeorm-upsert-create-if-not-exist

## TODO

- Seed via migrations API: https://stackoverflow.com/questions/51198817/typeorm-how-to-seed-database
- Try https://github.com/doug-martin/nestjs-query
