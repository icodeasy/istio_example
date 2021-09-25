# 说明
- consistent_by_query_param.yaml 用来测试通过请求参数进行一致性hash路由
		
		curl http://192.168.99.100:30001/svc2?uid=1
		会固定访问v2版本的pod
		curl http://192.168.99.100:30001/svc2?uid=3
		会固定访问v1版本的pod

- consistent_by_head.yaml 对service2 应用一致性hash 通过request header, 在多版本的服务做验证，是因为通过kiali可以比较清楚看出来流量到哪里了
	
		curl --header "uid:3" http://192.168.99.100:30001/svc2 
		只会到v1的subset
		curl --header "uid:1" http://192.168.99.100:30001/svc2 
		只会到v2的subset