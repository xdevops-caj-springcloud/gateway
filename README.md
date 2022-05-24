[TOC]

# Demo for Spring Cloud Gateway

## References

- [Spring Guides | Building a Gateway](https://spring.io/guides/gs/gateway/)
- [Spring Cloud Gateway Document](https://cloud.spring.io/spring-cloud-gateway/reference/html/)
- [Other references](./HELP.md)

## Tools
- [HTTPie](https://github.com/httpie/httpie)
- [httpbin](http://httpbin.org/)

## 路由(route)配置

路由配置方式：
- 代码：Java API (本demo)
- 配置文件：Application configuration file (application.properties或application.yaml)
- 路由发现：Route Discovery （需要配置服务注册中心使用）

Route predicate:
- path 路径
- host 主机名

## 过滤器（Filter）配置

## 测试
用HTTPie来测试

### Test a simple route
```bash
# test via path
http :8080/get
```

### Test Spring Cloud CircuitBreaker

```
# test via host
# circutit breaker without fallback: 503 Gateway Timeout
# circutit breaker with fallback: 200 OK
http -v :8080/delay/3 Host:'www.circuitbreaker.com'
```

Test fallback:
