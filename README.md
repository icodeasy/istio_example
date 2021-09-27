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
- lowConnectionPoolService 用来测试istio的流量过载短路
- outlierService 用来测试istio的异常值检测短路

		使用offical的fortio-deploy进行测试，方便统计响应码
		1 kubectl apply -f samples/httpbin/sample-client/fortio-deploy.yaml 位于istio安装目录下
		2 export FORTIO_POD=$(kubectl get pods -l app=fortio -o 'jsonpath={.items[0].metadata.name}')
		3 k exec "$FORTIO_POD" -c fortio -- /usr/bin/fortio load -c 2 -qps 0 -n 20 -loglevel Warning http://outlier-service/500

		