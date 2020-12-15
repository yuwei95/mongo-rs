1.各主机分别安装mongodb

2.修改配置文本mongo.conf:

    net:
      port: 27017
      bindIp: 192.168.88.128,localhost  # Enter 0.0.0.0,:: to bind to all IPv4 and IPv6 addresses or, alternatively, use the net.bindIpAll setting.
    
    #security:
    #operationProfiling:
    replication:
      replSetName: rs0   # 副本集名称，所有主机相同

3.各主机启动mongodb,sudo systemctl start mongod
4.在主节点执行：

    rsconf={
    	"_id": "rs0",
    	"members": [{
    		"_id": 0,
    		"host": "192.168.88.128:27017"
    	},
    	{
    		"_id": 1,
    		"host": "192.168.88.130:27017"
    	},
    	{
    		"_id": 2,
    		"host": "192.168.88.131:27017"
    	}]
    }
上面是几个主机制HOST+PORT
5.继续执行rs初始化:

    rs.initiate(rsconf)
6.最后查看副本集:

    rs.conf()
    rs.status()


