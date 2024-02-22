# camel-rest-dsl-test
Testing Camel Rest DSL with different OpenAPI schemas

<!-- Table of contents -->
## Index
- [Generating the Camel Rest DSL](#generating-the-camel-rest-dsl)
    - ✅ [`openapi-3.0.2.json` or `openapi-3.0.2.yaml`](#-openapi-302json-or-openapi-302yaml)
    - ❌ [`swagger-2.0.json` or `swagger-2.0.yaml`](#-swagger-20json-or-swagger-20yaml)
- [Running the example route using the `--open-api` modifier](#running-the-example-route-using-the---open-api-modifier)
  - ✅ [`openapi-3.0.2.json` or `openapi-3.0.2.yaml`](#-openapi-302json-or-openapi-302yaml)
  - ✅ [`swagger-2.0.json` or `swagger-2.0.yaml`](#-swagger-20json-or-swagger-20yaml)

## Generating the Camel Rest DSL out of the OpenAPI schema
### ✅ `openapi-3.0.2.json` or `openapi-3.0.2.yaml`
```bash
$ camel generate rest --input ./OpenAPI/openapi-3.0.2.json --output rest-openapi-3.0.yaml
# Sucess

$ camel generate rest --input ./OpenAPI/openapi-3.0.2.yaml --output rest-openapi-3.0.yaml
# Sucess
```

### ❌ `swagger-2.0.json` or `swagger-2.0.yaml`
```bash
$ camel generate rest --input ./OpenAPI/swagger-2.0.json --output rest-swagger-2.0.yaml
# Error
```
This command throws an exception:
```log
java.lang.ClassCastException: class io.apicurio.datamodels.models.openapi.v20.OpenApi20DocumentImpl cannot be cast to class io.apicurio.datamodels.models.openapi.v30.OpenApi30Document (io.apicurio.datamodels.models.openapi.v20.OpenApi20DocumentImpl and io.apicurio.datamodels.models.openapi.v30.OpenApi30Document are in unnamed module of loader 'app')
        at org.apache.camel.dsl.jbang.core.commands.CodeRestGenerator.doCall(CodeRestGenerator.java:74)
        at org.apache.camel.dsl.jbang.core.commands.CamelCommand.call(CamelCommand.java:71)
        at org.apache.camel.dsl.jbang.core.commands.CamelCommand.call(CamelCommand.java:37)
        at picocli.CommandLine.executeUserObject(CommandLine.java:2041)
        at picocli.CommandLine.access$1500(CommandLine.java:148)
        at picocli.CommandLine$RunLast.executeUserObjectOfLastSubcommandWithSameParent(CommandLine.java:2461)
        at picocli.CommandLine$RunLast.handle(CommandLine.java:2453)
        at picocli.CommandLine$RunLast.handle(CommandLine.java:2415)
        at picocli.CommandLine$AbstractParseResultHandler.execute(CommandLine.java:2273)
        at picocli.CommandLine$RunLast.execute(CommandLine.java:2417)
        at picocli.CommandLine.execute(CommandLine.java:2170)
        at org.apache.camel.dsl.jbang.core.commands.CamelJBangMain.run(CamelJBangMain.java:151)
        at org.apache.camel.dsl.jbang.core.commands.CamelJBangMain.run(CamelJBangMain.java:58)
        at main.CamelJBang.main(CamelJBang.java:36)
```
The same happens for the YAML version of the swagger file.


## Running the example route using the `--open-api` modifier

### ✅ `openapi-3.0.2.json` or `openapi-3.0.2.yaml`
```bash
# Run the following command in one terminal
$ camel run --open-api ./OpenAPI/swagger-2.0.json run *

# Alternatively, we could use the YAML file instead
$ camel run --open-api ./OpenAPI/swagger-2.0.yaml run *

```
Output:
```log
...
2024-02-22 12:04:19.080  INFO 68748 --- [ntloop-thread-0] .http.vertx.VertxPlatformHttpServer : Vert.x HttpServer started on 0.0.0.0:8080
2024-02-22 12:04:19.167  INFO 68748 --- [           main] el.impl.engine.AbstractCamelContext : Routes startup (started:2)
2024-02-22 12:04:19.168  INFO 68748 --- [           main] el.impl.engine.AbstractCamelContext :     Started route-9248 (direct://greeting-api)
2024-02-22 12:04:19.168  INFO 68748 --- [           main] el.impl.engine.AbstractCamelContext :     Started greeting-api (rest://get:/camel/:/greetings/%7Bname%7D)
2024-02-22 12:04:19.168  INFO 68748 --- [           main] el.impl.engine.AbstractCamelContext : Apache Camel 4.4.0 (example-route) started in 472ms (build:0ms init:0ms start:472ms)
2024-02-22 12:04:19.169  INFO 68748 --- [           main] t.platform.http.main.MainHttpServer : HTTP endpoints summary
2024-02-22 12:04:19.171  INFO 68748 --- [           main] t.platform.http.main.MainHttpServer :     http://0.0.0.0:8080/camel/greetings/{name} (GET)
```

From a different terminal, we make a Rest request to that endpoint:
```bash
curl localhost:8080/camel/greetings/Camel
```
Camel CLI Output:
```log
# 2024-02-22 12:00:26.750  INFO 4628 --- [worker-thread-0] example-route.yaml:10               : The endpoint was triggered
```

### ✅ `swagger-2.0.json` or `swagger-2.0.yaml`
```bash
# Run the following command in one terminal
$ camel run --open-api ./OpenAPI/swagger-2.0.json run *

# Alternatively, we could use the YAML file instead
$ camel run --open-api ./OpenAPI/swagger-2.0.yaml run *

```
Output:
```log
...
2024-02-22 12:03:47.965  INFO 57672 --- [ntloop-thread-0] .http.vertx.VertxPlatformHttpServer : Vert.x HttpServer started on 0.0.0.0:8080
2024-02-22 12:03:48.052  INFO 57672 --- [           main] el.impl.engine.AbstractCamelContext : Routes startup (started:2)
2024-02-22 12:03:48.052  INFO 57672 --- [           main] el.impl.engine.AbstractCamelContext :     Started route-9248 (direct://greeting-api)
2024-02-22 12:03:48.053  INFO 57672 --- [           main] el.impl.engine.AbstractCamelContext :     Started greeting-api (rest://get:/camel/:/greetings/%7Bname%7D)
2024-02-22 12:03:48.053  INFO 57672 --- [           main] el.impl.engine.AbstractCamelContext : Apache Camel 4.4.0 (example-route) started in 458ms (build:0ms init:0ms start:458ms)
2024-02-22 12:03:48.054  INFO 57672 --- [           main] t.platform.http.main.MainHttpServer : HTTP endpoints summary
2024-02-22 12:03:48.056  INFO 57672 --- [           main] t.platform.http.main.MainHttpServer :     http://0.0.0.0:8080/camel/greetings/{name} (GET)
```

From a different terminal, we make a Rest request to that endpoint:
```bash
curl localhost:8080/camel/greetings/Camel
```
Camel CLI Output:
```log
# 2024-02-22 12:00:26.750  INFO 4628 --- [worker-thread-0] example-route.yaml:10               : The endpoint was triggered
```
