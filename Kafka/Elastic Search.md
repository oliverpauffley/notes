# Elastic Search
Elastic search is a distributed database system to allow easy searching using indices. Everything can be controlled through rest api calls.

## Creating New Indexes
PUT -` <url>/<index-name> `

## Insert
To insert data you need to write a PUT request to `<url>/<index-name>/<document-type>/<uuid>`in a json format. eg

PUT `/twitter/tweets/1`
```json
{
  "course": "Kafka for Beginners",
  "instructor": "Stpanne Maarek",
  "module": "ElasticSearch"
}
```

## Get
GET `<url>/<index-name>/<document-type>/<uuid>`

## Delete
DELETE`<url>/<index-name>/<document-type>/<uuid>`