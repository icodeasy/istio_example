# istio_example
as a record book for learning istio
基于1.9.8

# set up 
- 可视化 kubectl apply -f istio-1.9.8/samples/addons/kiali.yaml
- 数据源 因为 kiali.yaml 依赖prometheus作为数据源，所以同时也需要apply istio-1.9.8/samples/addons/prometheus.yaml
- 启动  istioctl dashboard kiali

# 说明
- service2 用来在kiali展示多版本的路由
- service1 作为其他demo服务的入口
- svc2_destinationrule.yaml 对service2 应用round robin 和random lb规则

		