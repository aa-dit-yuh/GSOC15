- **GET** /api/tasks  
  Returns a list of tasks in the queue.  
  Example request:  
  ```http
  GET /api/tasks HTTP/1.1
  Host: localhost:5555
  User-Agent: HTTPie/0.8.0
  ```  
  Example response:  
  ```json
  HTTP/1.1 200 OK
  Content-Length: 1109
  Content-Type: application/json; charset=UTF-8
  Etag: "b2478118015c8b825f7b88ce6b660e5449746c37"
  Server: TornadoServer/3.1.1
  
  {
    "e42ceb2d-8730-47b5-8b4d-8e0d2a1ef7c9": {
        "args": "{'atom_data':'...',...}",
        "client": null,
        "clock": 1079,
        "eta": null,
        "exception": null,
        "exchange": null,
        "expires": null,
        "failed": null,
        "kwargs": "{}",
        "name": "tasks.1Dspectrum",
        "received": 1398505411.107885,
        "result": "http://example.com/run/e42ceb2d-8730-47b5-8b4d-8e0d2a1ef7c9",
        "retried": null,
        "retries": 0,
        "revoked": null,
        "routing_key": null,
        "runtime": 0.01610181899741292,
        "sent": null,
        "started": 1398505411.108985,
        "state": "SUCCESS",
        "succeeded": 1398505411.124802,
        "timestamp": 1398505411.124802,
        "traceback": null,
        "uuid": "e42ceb2d-8730-47b5-8b4d-8e0d2a1ef7c9"
    },
    "f67ea225-ae9e-42a8-90b0-5de0b24507e0": {
        "args": "{'atom_data':'...',...}",
        "client": null,
        "clock": 1042,
        "eta": 360,
        "exception": null,
        "exchange": null,
        "expires": null,
        "failed": null,
        "kwargs": "{}",
        "name": "tasks.1Dspectrum",
        "received": 1398505395.327208,
        "result": "http://example.com/run/f67ea225-ae9e-42a8-90b0-5de0b24507e0",
        "retried": true,
        "retries": 1,
        "revoked": null,
        "routing_key": null,
        "runtime": 0.012884548006695695,
        "sent": null,
        "started": 1398505395.3289,
        "state": "PENDING",
        "succeeded": 1398505395.341089,
        "timestamp": 1398505395.341089,
        "traceback": null,
        "uuid": "f67ea225-ae9e-42a8-90b0-5de0b24507e0"
    }
  }
  ```
  Query Parameters:  
    limit: maximum number of tasks listed, default=10  
    state: filter by state(SUCCESS, FAILURE, PENDING)  
- **GET** /api/task/info/(task UUID)  
  Get a task info  
  Example request:  
  ```http
  GET /api/task/info/91396550-c228-4111-9da4-9d88cfd5ddc6 HTTP/1.1
  Accept: */*
  Accept-Encoding: gzip, deflate, compress
  Host: localhost:5555
  ```  
  Example response:  
  ```json
  HTTP/1.1 200 OK
  Content-Length: 575
  Content-Type: application/json; charset=UTF-8

  {
    "args": "[2, 2]",
    "client": null,
    "clock": 25,
    "eta": null,
    "exception": null,
    "exchange": null,
    "expires": null,
    "failed": null,
    "kwargs": "{}",
    "name": "tasks.add",
    "received": 1400806241.970742,
    "result": "'4'",
    "retried": null,
    "retries": null,
    "revoked": null,
    "routing_key": null,
    "runtime": 2.0037889280356467,
    "sent": null,
    "started": 1400806241.972624,
    "state": "SUCCESS",
    "succeeded": 1400806243.975336,
    "task-id": "91396550-c228-4111-9da4-9d88cfd5ddc6",
    "timestamp": 1400806243.975336,
    "traceback": null,
    "worker": "worker1"
  }
  ```
- **POST** /api/task/aync-apply/  
  Execute a task  
  Example request:  
  ```http
  POST /api/task/async-apply/tasks.add HTTP/1.1
  Accept: application/json
  Accept-Encoding: gzip, deflate, compress
  Content-Length: 46
  Content-Type: application/json; charset=utf-8
  Host: localhost:5555
  
  {
    "args": "{'atom_data':...,
              'model':...,
            }"
  }
  ```  
  Example response:  
  ```json
  HTTP/1.1 200 OK
  Content-Length: 71
  Content-Type: application/json; charset=UTF-8
  Date: Sun, 13 Apr 2014 15:55:00 GMT
  
  {
    "state": "PENDING",
    "task-id": "abc300c7-2922-4069-97b6-a635cc2ac47c"
  }
  ```  
- **POST** /api/task/revoke/(task UUID)  
  Revoke a task   
  Example request:
  ```http
  POST /api/task/revoke/1480b55c-b8b2-462c-985e-24af3e9158f9
  Content-Length: 0
  Content-Type: application/x-www-form-urlencoded; charset=utf-8
  Host: localhost:5555
  ```  
  Example response:  
  ```json
  HTTP/1.1 200 OK
  Content-Length: 61
  Content-Type: application/json; charset=UTF-8

  {
    "message": "Revoked '1480b55c-b8b2-462c-985e-24af3e9158f9'"
  }
  ```
