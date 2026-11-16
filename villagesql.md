# VillageSQL Skills

Desenvolvimento de extensoes, compatibilidade com PostgreSQL e engenharia de extensoes VillageSQL.

## O que e VillageSQL

Framework para criacao de extensoes PostgreSQL com foco em facilidade de desenvolvimento e manutencao.

## Arquitetura de Extensoes

### Estrutura Padrao
my_extension/
  Cargo.toml (para Rust)
  control file
  sql/
    my_extension--1.0.sql
  src/
    lib.rs
  tests/

### Componentes
- **SQL files:** definicoes de schema, funcoes
- **Control file:** metadados da extensao
- **Source code:** implementacao em C/Rust
- **Tests:** testes de integracao

## Desenvolvimento com Rust (pgrx)

### Setup
cargo install cargo-pgrx
cargo pgrx init
cargo pgrx new my_extension

### Funcoes SQL
#[pg_extern]
fn add_numbers(a: i32, b: i32) -> i32 {
    a + b
}

### Tipos Customizados
#[derive(PostgresType)]
struct Point {
    x: f64,
    y: f64,
}

### Agregacoes
#[pg_aggregate]
impl Aggregate for MyAvg {
    // implementacao
}

### Triggers
#[pg_trigger]
fn audit_trigger() {
    // logica
}

## Desenvolvimento com C

### Estrutura Basica
#include "postgres.h"
#include "fmgr.h"

PG_MODULE_MAGIC;

PG_FUNCTION_INFO_V1(my_function);

Datum my_function(PG_FUNCTION_ARGS) {
    // implementacao
    PG_RETURN_INT32(result);
}

### Makefile
MODULE = my_extension
EXTENSION = my_extension
DATA = my_extension--1.0.sql

PG_CONFIG = pg_config
PGXS := $(shell $(PG_CONFIG) --pgxs)
include $(PGXS)

## Compatibilidade PostgreSQL

### Versoes Suportadas
- PostgreSQL 12+
- Testar em multiplas versoes
- Version-specific features

### Best Practices
- Use PG_TRY/PG_CATCH para error handling
- Memory management com palloc/pfree
- SPI (Server Programming Interface) para queries
- Background workers para tasks assincronas

## Testing

### pgrx Tests
#[cfg(any(test, feature = "pg_test"))]
#[pg_test]
fn test_add_numbers() {
    assert_eq!(add_numbers(2, 3), 5);
}

### Integration Tests
- pg_regress para SQL tests
- Docker para isolated environments
- CI/CD com GitHub Actions

## Deployment

### Packaging
- Criar .deb/.rpm packages
- Docker images
- Extension versioning

### Installation
CREATE EXTENSION my_extension;

### Updates
ALTER EXTENSION my_extension UPDATE TO '2.0';

## Seguranca

- Input validation
- SQL injection prevention
- Privilege management
- Audit logging

## Performance

- Index strategies
- Query optimization
- Caching
- Parallel execution

## Recursos
- pgrx documentation
- PostgreSQL extension documentation
- VillageSQL examples