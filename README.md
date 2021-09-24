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
- svc2_consistenthash_dr.yaml 对service2 应用一致性hash 通过request header, 在多版本的服务做验证，是因为通过kiali可以比较清楚看出来流量到哪里了
	
		curl --header "uid:3" http://192.168.99.100:30001/svc2 
		只会到v1的subset
		curl --header "uid:1" http://192.168.99.100:30001/svc2 
		只会到v2的subset
		