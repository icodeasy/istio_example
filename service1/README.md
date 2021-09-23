# 说明
- service1 作为所有微服务的入口服务
- 意图是用nginx仿造微服务
- 使用configmap灵活配置nginx

# 使用
- k get node 获得node的internal ip
- 由于是测试，所以直接通过nodePort 暴露service1 的端口
- 通过 curl http://${node internal ip}:${nodePort} 查看结果

# 注意
- 在istio envoy启用后，通过ngnix转发请求到对应的service，需要设置 proxy_http_version 1.1， 因为  Istio 使用 Envoy 作为数据面转发 HTTP 请求，而 Envoy 默认要求使用 HTTP/1.1 或 HTTP/2，当客户端使用 HTTP/1.0 时就会返回 426 Upgrade Required。