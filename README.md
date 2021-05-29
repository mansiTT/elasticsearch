
# Elasticsearch Frequently used commands

### List indexes

```javascript
curl --location --request GET 'http://localhost:9200/_cat/indices' 
```

### Create Index CURL :

```javascript
curl --location --request PUT 'http://localhost:9200/employee' 

Response 200:
```
{"acknowledged":true,"shards_acknowledged":true,"index":"employee"}
```
```


### Add document in index

```javascript
curl --location --request POST 'http://localhost:9200/employee/_doc' \
--header 'Content-Type: application/json' \
--data-raw '{
    "employeeNo": 1,
    "firstname": "john",
    "lastname": "doe",
    "designation": "Lead Engineer",
    "department": {
        "id": 1,
        "name": "HR"
    },
    "manager": {
        "id": 1
    },
    "skills": [
        "backend",
        "frontend",
        "react",
        "reactjs",
        "node"
    ],
    "dateOfBirth": "1990-05-18",
    "dateOfJoining": "2021-03-20",
    "lastOrganisations": [
        {
            "name": "xyz corp",
            "profile": {
                "designation": "Senior Engineer",
                "skills": []
            },
            "lwd": "2021-01-31",
            "dateOfJoining": "2021-03-20"
        }
    ]
}'
```
Response 201 :
```
{
    "_index": "employee",
    "_type": "_doc",
    "_id": "Gc7AsXkBTEi-c2akxw-x",
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 0,
    "_primary_term": 1
}
```



### Search document in index 

```javascript
curl --location --request GET 'http://localhost:9200/employee/_search' 
```

Response 200 :
```
{
    "took": 1144,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "employee",
                "_type": "_doc",
                "_id": "Gc7AsXkBTEi-c2akxw-x",
                "_score": 1.0,
                "_source": {
                    "employeeNo": 1,
                    "firstname": "john",
                    "lastname": "doe",
                    "designation": "Lead Engineer",
                    "department": {
                        "id": 1,
                        "name": "HR"
                    },
                    "manager": {
                        "id": 1
                    },
                    "skills": [
                        "backend",
                        "frontend",
                        "react",
                        "reactjs",
                        "node"
                    ],
                    "dateOfBirth": "1990-05-18",
                    "dateOfJoining": "2021-03-20",
                    "lastOrganisations": [
                        {
                            "name": "xyz corp",
                            "profile": {
                                "designation": "Senior Engineer",
                                "skills": []
                            },
                            "lwd": "2021-01-31",
                            "dateOfJoining": "2021-03-20"
                        }
                    ]
                }
            }
        ]
    }
}
```

### Count documents in index

```javascript
http://localhost:9200/employee/_count
```
```
Response 200:

{
    "count": 1,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    }
}
```

### Search with From/Size (Pagination)

```javascript
curl --location --request GET 'http://localhost:9200/employee/_search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "from" : 0, "size" : 100
}'
```

### Search with Criteria

```javascript
curl --location --request GET 'http://localhost:9200/employee/_search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "query": {
        "match" : {
            "firstname" : "John"
        }
    }
}'
```



