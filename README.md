[TOC]

# Demo for Spring Cloud Gateway

## References

- [Spring Guides | Building a Gateway](https://spring.io/guides/gs/gateway/)
- [Spring Cloud Gateway Document](https://cloud.spring.io/spring-cloud-gateway/reference/html/)
- [Other references](./HELP.md)

## Tools
- [HTTPie](https://github.com/httpie/httpie)
- [httpbin](http://httpbin.org/)

## Key Concepts

<https://cloud.spring.io/spring-cloud-gateway/reference/html/#glossary>

Key Concepts:
- Route
- Predicate
- Filter: Gateway Filter

## 路由(route)配置

路由配置方式：
- 代码：[Java API](https://cloud.spring.io/spring-cloud-gateway/reference/html/#fluent-java-routes-api) (本demo)
- 配置文件：Application configuration file (application.properties或application.yaml)
- 路由发现：[Route Discovery](https://cloud.spring.io/spring-cloud-gateway/reference/html/#the-discoveryclient-route-definition-locator) （需要配置服务注册中心使用）

Route predicate:
- Path 路径
- Host 主机名

## 过滤器（Filter）配置

Filters:
- addRequestHeader
- circuitBreaker
- fallback

Global filters:
- ForwarRoutingdFilter: `forward:/fallback`

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

## Further reading

### Route predicate list

Route predicate list:
- After/Before/Between: datetime
- Cookie
- Header
- Host
- Method: HTTP methods to match
- Query: Query parameters
- RemoteAddr
- Weight: 按照权重分配路由的流量

<https://cloud.spring.io/spring-cloud-gateway/reference/html/#gateway-request-predicates-factories>

### Gateway Filter list

Gateway Filter list:
- AddRequestHeader
- AddRequestParameter
- AddResponseHeader
- DedupeResponseHeader
- Spring Cloud CircuitBreaker
- FallbackHeaders
- MapRequestHeader
- PrefixPath
- PreserveHostHeader
- RequestRateLimiter
- Redis RateLimiter
- RedirectTo
- RemoveRequestHeader
- RemoveResponseHeader
- RemoveRequestParameter
- RewritePath
- RewriteLocationResponseHeader
- RewriteResponseHeader
- SaveSession
- SecureHeaders
- SetPath
- SetRequestHeader
- SetResponseHeader
- SetStatus
- StripPrefix
- Retry
- RequestSize
- SetRequestHost
- ModifyRequestBody
- ModifyResponseBody


Route filters allow the **modification of the incoming HTTP request or outgoing HTTP response** in some manner. Route filters are scoped to a particular route.
Spring Cloud Gateway includes many built-in GatewayFilter Factories.

<https://cloud.spring.io/spring-cloud-gateway/reference/html/#gatewayfilter-factories>

Default filters:
To add a filter and apply it to all routes, you can use spring.cloud.gateway.default-filters

Global filters:
- ForwardRoutingFilter
- LoadBalanceClientFilter
- ReactiveLoadBalancerClientFilter
- Netty Routing Filter
- Netty Write Response Filter
- RouteToRequestUrlFilter
- Websocket Routing Filter
- Gateway Metrics Filter

Schema:
- `forward://` - Forward
- `lb://` - Load balance
- `ws://` - Websocket