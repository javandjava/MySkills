### skywalking

#### agent
#### collector
#### alarm
#### traceid

#### graphql

##### Duration
1. 时间区间
```
"duration":{
    "start": "2020-07-10 1400", 
    "end": "2020-07-10 1400", 
    "step": "MINUTE" # MONTH DAY HOUR MINUTE SECOND
}
```

2. service
```
{
  id
  name
}
```

3. Scope
- Service
- ServiceInstance
- Endpoint 


##### 查询service :searchServices(duration:$duration,keyword:$keyword)
1. graphql
```

query q($duration:Duration!,$keyword:String!){
    services:searchServices(duration:$duration,keyword:$keyword)
    {
        key:id 
        label:name
    }
}

{
"duration":
{"start": "2020-07-13 1000", 
"end": "2020-07-13 1100", 
"step": "MINUTE"},
"keyword":""
}
```

2. json
```
{"query":"query queryServices($duration: Duration!,$keyword: String!) {services: searchServices(duration: $duration, keyword: $keyword) {      key: id      label: name}}","variables":{"duration":{"start":"2020-07-13 0957","end":"2020-07-13 1057","step":"MINUTE"},"keyword":""}}
```

3. 返回
```
"data": {
        "services": [
            {
                "key": "c2VhbF9leGFtXyhzdW1tZXIpXzE3Mi4yNi4xMzAuNA==.1",
                "label": "seal_exam_(summer)_172.26.130.4"
            },
            {
                "key": "c2VhbF9mcm9udGVuZF8oYXV0dW1uKV8xNzIuMjYuMTMwLjk=.1",
                "label": "seal_frontend_(autumn)_172.26.130.9"
            }
        ]
}
```

##### sortMetrics 查询
1. ql
```
query q($condition:TopNCondition!,$duration:Duration!){
    avg:sortMetrics(condition: $condition,duration:$duration)
    {
            name
            id
            value
            
    }
}
```

2. variabels
```
{
"duration":
    {"start": "2020-07-13 1930", 
    "end": "2020-07-13 1935", 
    "step": "MINUTE"},
"condition":{
    "name": "endpoint_avg",
    "normal": true,
    "order": "DES",
    "parentService": null,
    "scope": "Endpoint",
    "topN": 100
    }
}
```

3. respnose
```
{
    "data": {
        "avg": [
            {
                "name": "seal_exam_(friday)_172.26.130.42 - /exam/api/collections_suit/publish/pub",
                "id": "c2VhbF9leGFtXyhmcmlkYXkpXzE3Mi4yNi4xMzAuNDI=.1_L2V4YW0vYXBpL2NvbGxlY3Rpb25zX3N1aXQvcHVibGlzaC9wdWI=",
                "value": "635"
            },
            {
                "name": "seal_word_(env2) - /word/data/getWordAll",
                "id": "c2VhbF93b3JkXyhlbnYyKQ==.1_L3dvcmQvZGF0YS9nZXRXb3JkQWxs",
                "value": "337"
            },
            {
                "name": "seal_exam_(summer)_172.26.130.4 - /exam/app/api/teacherClass",
                "id": "c2VhbF9leGFtXyhzdW1tZXIpXzE3Mi4yNi4xMzAuNA==.1_L2V4YW0vYXBwL2FwaS90ZWFjaGVyQ2xhc3M=",
                "value": "301"
            },
            {
                "name": "seal_homework_manager_(summer)_172.26.130.137 - /feign/wechat/api/collection_suit/statistics_result4App",
                "id": "c2VhbF9ob21ld29ya19tYW5hZ2VyXyhzdW1tZXIpXzE3Mi4yNi4xMzAuMTM3.1_L2ZlaWduL3dlY2hhdC9hcGkvY29sbGVjdGlvbl9zdWl0L3N0YXRpc3RpY3NfcmVzdWx0NEFwcA==",
                "value": "218"
            },
            {
                "name": "seal_exam_(env2) - /exam/wx/api/exercise/plan/student/listStudentTaskPlan",
                "id": "c2VhbF9leGFtXyhlbnYyKQ==.1_L2V4YW0vd3gvYXBpL2V4ZXJjaXNlL3BsYW4vc3R1ZGVudC9saXN0U3R1ZGVudFRhc2tQbGFu",
                "value": "204"
            }
        ]
    }
}
```

4. 可查询的
- service_resp_time
- service_sla
- service_cpm
- service_instance_sla
- service_instance_resp_time
- service_instance_cpm
- endpoint_cpm
- endpoint_avg
- endpoint_sla
- instance_jvm_cpu
- instance_jvm_memory_heap
- instance_jvm_memory_heap_max

-  更多 https://github.com/apache/skywalking/blob/master/oap-server/oal-rt/src/test/resources/oal_test.oal