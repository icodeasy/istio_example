# istio_example
as a record book for learning istio
基于1.9.8

# set up 
- 可视化 kubectl apply -f istio-1.9.8/samples/addons/kiali.yaml
- 数据源 因为 kiali.yaml 依赖prometheus作为数据源，所以同时也需要apply istio-1.9.8/samples/addons/prometheus.yaml
- 启动  istioctl dashboard kiali