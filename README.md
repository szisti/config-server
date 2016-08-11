**Configuration:**  
```
spring.cloud.config.server.git.uri=https://github.com/szisti/config
spring.cloud.config.server.git.search-paths[0]=/
spring.cloud.config.server.git.search-paths[1]={application}
spring.cloud.config.server.git.search-paths[2]={application}/{profile}

spring.cloud.config.server.git.repos.test.pattern=test*
spring.cloud.config.server.git.repos.test.uri=https://github.com/szisti/config
spring.cloud.config.server.git.repos.test.searchPaths=test,test/{profile}
```

**URL:**  
http://localhost:8888/test-123/agt  

**Response:**  
```
{
   	name: "test-123",
   	profiles: ["agt"],
   	label: "master",
   	version: "d233d4b9906f8c6da6b4b56b575afa038c23c6ca",
   	propertySources: [{
   		name: "https://github.com/szisti/config/test/agt/test-123.properties",
   		source: {
   			server.port: "8082"
   		}
   	},
   	{
   		name: "https://github.com/szisti/config/test/agt/application.properties",
   		source: {
   			server.port: "8081",
   			spring.cloud.zookeeper.connect-string: "zookeeper01agt.ew1.vcint.com:2181/discovery"
   		}
   	},
   	{
   		name: "https://github.com/szisti/config/test/application.properties",
   		source: {
   			server.port: "${PORT:8080}",
   			spring.cloud.zookeeper.connect-string: "localhost:2181"
   		}
   	},
   	{
   		name: "https://github.com/szisti/config/application.properties",
   		source: {
   			server.port: "${PORT:0}"
   		}
   	}]
   }
```
   
**URL:**  
http://localhost:8888/test-123-agt.properties  

**Response:**  
```
server.port: 8081
spring.cloud.zookeeper.connect-string: zookeeper01agt.ew1.vcint.com:2181/discovery
```

**Expected response:**  
```
server.port: 8082
spring.cloud.zookeeper.connect-string: zookeeper01agt.ew1.vcint.com:2181/discovery
```