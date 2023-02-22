# Java

- [WebClient](#WebClient)

## WebClient

```java

    private WebClient businessClient;

    @Autowired
    public void setBusinessClient(WebClient.Builder builder, ReactorLoadBalancerExchangeFilterFunction filterFunction) {
        this.businessClient = builder.baseUrl("http://quick-books-business/")
                .filter(filterFunction)
                .build();
    }
```
