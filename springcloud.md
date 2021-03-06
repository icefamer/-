### 负载均衡的机制：轮询，哈希，随机等等

### 客户端发现指注册中心接收到服务调用请求后通过负载均衡机制找到一个可用的服务提供方的IP，然后调用。

### 服务端发现指服务端代理帮助客户端找到可用的地址再给客户端让它来调用

### 客户端发现优点：调用简单，不需要额外的代理介入，知道所有服务端的地址；缺点：需要自己实现一套逻辑来找到可用的服务端地址。

### 服务端发现优点：服务端地址对客户端不可见，只需要找代理就行。

### 客户端代理注册中心：Eureka；服务端代理注册中心：zookeeper，nginx等

### 微服务开发以产品为导向，一个产品团队负责整个服务的前端到后台一系列工程，这个跟传统的资源业务团队模式很不一样。

### springboot测试有两种注解引入方法，@RunWith(SpringRunner.class) @SpringBootTest；以及@Component然后测试方法继承项目主方法测试类。

### springCloud的客户端负载均衡就是ribbon组件，能提供高效的软负载机制，运作流程为：
  1. 依据服务名字把所有该服务的可用服务列表找出来（ServerList）
  2. 根据轮询（默认），哈希，随机等具体的策略从所有服务节点中选择一个服务提供方(IRule)
  3. 检测失效的服务，高效剔除(ServerListFilter)

### Feign是一个声明式REST客户端（伪RPC），基于接口的注解。

### 无参数或是单个参数（@RequestParament）的时候可以使用@GetMapping，其他的（@RequestBody）使用@PostMapping

### 消息队列常见应用场景：
  - 异步处理
  - 流量控制：将同一时间涌入的多余流量抛弃或转向错误页面（秒杀）
  - 日志处理：将日志文件定时写入消息队列后进行接收储存和转发
  - 应用解耦：服务直接本来是通过接口进行耦合的，现在只需要把请求发送到队列里由消息队列进行后续的处理。

### 服务网关是所有客户端请求的入口，所有非业务操作的绝佳处理场所，诸如协议转发，防刷，流量管控，日志监控等。

### zuul的过滤器：
  - pre-filter：前置过滤器，主要用处，限流（令牌桶限流）、鉴权、参数校验调整
  - route-filter: 将外部请求转发到origin server去
  - post-filter: 后置过滤器，统计、日志记录
  - error-filter: 上面三个过滤器发生异常后到达这里
  - 还有自定义filter，随意放到其他地方。

### 跨域范围，cookie跨域，方法，头，服务：
  - 在类或方法上添加@CrossOrigin注解
  - 在zuul里增加CorsFilter过滤器

### 雪崩效应：某个服务不可用引起连锁反应导致整个系统不可用，springCloud里防止雪崩效应的组件式hystrix，作用有：
  - 服务降级：优先核心服务，非核心服务不可用或弱可用
  - 依赖隔离：为每个依赖单独配置一个线程池，某一个服务的调用出现故障不会影响其他服务调用
  - 服务熔断：当失败率达到阀值会自动触发降级
  - 监控：实时监控，报警，控制等

### 链路监控，Sleuth组件：快速定位各服务响应状态

### 统一配置中心，ConfigServer服务名规则/{label}/{name}-{profiles}.json(yml)：
  - name：这个就是文件的名字
  - profiles: 环境，指的是哪种使用场景（测试，生产等）
  - label: git里面的分支