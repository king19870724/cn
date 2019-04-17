---
layout: default
title: Common application properties
permalink: /common-application-properties/
sitemap:
    priority: 0.7
    lastmod: 2018-03-18T18:20:00-00:00
---

# <i class="fa fa-flask"></i> 通用应用属性

JHipster生成的SpringBoot应用可以使用标准的SpringBoot配置文件机制。

这些配置在JHipster生成时创建，并且在开发和生产配置上配置不同，相关说明在[Profiles documentation]({{ site.url }}/profiles/).

在一个JHipster应用中，有3中配置文件

1. [Spring Boot standard application properties](#1)
2. [JHipster application properties](#2)
3. [Application-specific properties](#3)

## <a name="1"></a> SpringBoot标准应用配置文件

Like any Spring Boot application, JHipster allows you to configure any standard [Spring Boot application property](http://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html).
和其他Springboot应用一样，JHipster允许开发者配置标准的[SpringBoot应用配置](http://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html).

## <a name="2"></a> JHipster应用配置
 
JHipster也提供了特有的应用配置，详情可见 [JHipster server-side library](https://github.com/jhipster/jhipster)。这些配置也是JHipster的标准，但也有一部分依赖于你在创建项目时的选择：比如 `jhipster.cache.hazelcast` 只有在Hazelcast 你选择了2级hibernate缓存。

Those properties are configured using the `io.github.jhipster.config.JHipsterProperties` class.
这些配置使用类`io.github.jhipster.config.JHipsterProperties`创建。

Here is a documentation for those properties:
这是这些配置的文档：

    jhipster:

        # Thread pool that will be used for asynchronous method calls in JHipster
		# 用于JHipster异步方法调用的线程池
        async:
            core-pool-size: 2 # 初始大小
            max-pool-size: 50 # 最大容量
            queue-capacity: 10000 # 线程池最大队列量

		# JHipster网关的具体配置
		# 见 https://www.jhipster.tech/api-gateway/ 获取更多信息
        gateway:
            rate-limiting:
                enabled: false #是否在默认情况下禁用速率限制
                limit: 100_000L # 默认最多同时有100,000 API 
                duration-in-seconds: 3_600 # 默认速率限制每小时初始化一次
            authorized-microservices-endpoints: # 访问控制策略，如为空则全部节点都能访问
                app1: /api #推荐在生产环境下配置 这允许来自于“app1”微服务的全部请求

        # HTTP configuration
        http:
			# V_1_1 针对于 HTTP/1.1 or V_2_0 针对于 HTTP/2.
			# 为试用 HTTP/2 你需要用到ssl支持 （见 springboot 的server.ssl配置 ）
            version: V_1_1
            #强制服务端密码套件使用server.ssl.ciphers (为了完美的安全)
            useUndertowUserCipherSuitesOrder: true
            cache: #为 io.github.jhipster.web.filter.CachingHttpHeadersFilter 使用
                timeToLiveInDays: 1461 # 默认静态资源缓存4年

        #  缓存配置使用的Hibernate 2级缓存
        cache:
            hazelcast: # Hazelcast configuration
                time-to-live-seconds: 3600 # By default objects stay 1 hour in the cache
                backup-count: 1 # Number of objects backups
                # Configure the Hazelcast management center
                # Full reference is available at: http://docs.hazelcast.org/docs/management-center/3.9/manual/html/Deploying_and_Starting.html
                management-center:
                    enabled: false # Hazelcast management center is disabled by default
                    update-interval: 3 # Updates are sent to the Hazelcast management center every 3 seconds by default
                    # Default URL for Hazelcast management center when using JHipster's Docker Compose configuration
                    # See src/main/docker/hazelcast-management-center.yml
                    # Warning, the default port is 8180 as port 8080 is already used by JHipster
                    url: http://localhost:8180/mancenter
            ehcache: # Ehcache configuration
                time-to-live-seconds: 3600 # By default objects stay 1 hour in the cache
                max-entries: 100 # Number of objects in each cache entry
            infinispan: #Infinispan configuration
                config-file: default-configs/default-jgroups-tcp.xml
                # local app cache
                local:
                    time-to-live-seconds: 60 # By default objects stay 1 hour (in minutes) in the cache
                    max-entries: 100 # Number of objects in each cache entry
                #distributed app cache
                distributed:
                    time-to-live-seconds: 60 # By default objects stay 1 hour (in minutes) in the cache
                    max-entries: 100 # Number of objects in each cache entry
                    instance-count: 1
                #replicated app cache
                replicated:
                    time-to-live-seconds: 60 # By default objects stay 1 hour (in minutes) in the cache
                    max-entries: 100 # Number of objects in each cache entry
            # Memcached configuration
            # Uses the Xmemcached library, see https://github.com/killme2008/xmemcached
            memcached:
             # Disabled by default in dev mode, as it does not work with Spring Boot devtools
                enabled: true
                servers: localhost:11211 # Comma or whitespace separated list of servers' addresses
                expiration: 300 # Expiration time (in seconds) for the cache
                use-binary-protocol: true # Binary protocol is recommended for performance (and security)

        # E-mail properties
        mail:
            enabled: false # If e-mail sending is enabled. The standard `spring.mail` keys will need to be configured
            from: jhipster@localhost # The default "from" address for e-mails
            base-url: http://127.0.0.1:8080 # URL to the application, used inside e-mails

        # Spring Security specific configuration
        security:
            remember-me: # JHipster secure implementation of the remember-me mechanism, for session-based authentication
                # security key (this key should be unique for your application, and kept secret)
                key: 0b32a651e6a65d5731e869dc136fb301b0a8c0e4
            client-authorization: # Used with JHipster UAA authentication
                access-token-uri: # URL of the JHipster UAA server OAuth tokens
                token-service-id: # ID of the current application
                client-id: # OAuth client ID
                client-secret: # OAuth client secret
            authentication:
                jwt: # JHipster specific JWT implementation
                    # The secret token should be encoded using Base64 (you can type `echo 'secret-key'|base64` on your command line).
                    # If both properties are configured, the `secret` property has a higher priority than the `base64-secret` property.
                    secret: # JWT secret key in clear text (not recommended)
                    base64-secret:  # JWT secret key encoded in Base64 (recommended)
                    token-validity-in-seconds: 86400 # Token is valid 24 hours
                    token-validity-in-seconds-for-remember-me: 2592000 # Remember me token is valid 30 days

        # Swagger configuration
        swagger:
            default-include-pattern: /api/.*
            title: JHipster API
            description: JHipster API documentation
            version: 0.0.1
            terms-of-service-url:
            contact-name:
            contact-url:
            contact-email:
            license:
            license-url:
            host:
            protocols:

        # DropWizard Metrics configuration, used by MetricsConfiguration
        metrics:
            jmx: # Export metrics as JMX beans
                enabled: true # JMX is enabled by default
            # Send metrics to a Graphite server
            # Use the "graphite" Maven profile to have the Graphite dependencies
            graphite:
                enabled: false # Graphite is disabled by default
                host: localhost
                port: 2003
                prefix: jhipster
            # Send metrics to a Prometheus server
            prometheus:
                enabled: false # Prometheus is disabled by default
                endpoint: /prometheusMetrics
            logs: # Reports Dropwizard metrics in the logs
                enabled: false
                reportFrequency: 60 # frequency of reports in seconds

        # Logging configuration, used by LoggingConfiguration
        logging:
            logstash: # Forward logs to Logstash over a socket
                enabled: false # Logstash is disabled by default
                host: localhost # Logstash server URL
                port: 5000 # Logstash server port
                queue-size: 512 # Queue for buffering logs
            spectator-metrics: # Reports Netflix Spectator metrics in the logs
                enabled: false # Spectator is disabled by default

        # By default cross-origin resource sharing (CORS) is enabled in "dev" mode for
        # monoliths and gateways.
        # It is disabled by default in "prod" mode for security reasons, and for microservices
        # (as you are supposed to use a gateway to access them).
        # This configures a standard org.springframework.web.cors.CorsConfiguration
        # Note that "exposed-headers" is mandatory for JWT-based security, which uses
        # the "Authorization" header, and which is not a default exposed header.
        cors:
            allowed-origins: "*"
            allowed-methods: "*"
            allowed-headers: "*"
            exposed-headers: "Authorization"
            allow-credentials: true
            max-age: 1800

        # Ribbon displayed on the top left-hand side of JHipster applications
        ribbon:
            # Comma-separated list of profiles that display a ribbon
            display-on-active-profiles: dev

## <a name="3"></a> 特定的应用程序配置
 
生成的应用也可以有自己的springboot配置。这是优先推荐的，也是应用的类型安全的配置，同时在IDE中自动补全（配置）和生成文档 。

JHipster has generated a `ApplicationProperties` class in the `config` package, which is already preconfigured, and it is already documented at the bottom the `application.yml`, `application-dev.yml` and `application-prod.yml` files. All you need to do is code your own specific properties.
JHipster在 `config`包里面生成类`ApplicationProperties`，这个类已经做了预配置，同时也在`application.yml`, `application-dev.yml` 和 `application-prod.yml`文件的底部也做了文档。开发者所需要的做的是配置自己所要用的配置。