FORMAT: 1A
HOST: https://polls.apiblueprint.org/

# Maintenance

Simple API allowing users to view and manage theirs maintenance request.

## Maintenance by Branch Collection [/maintenance/{branchId}]

### List All Maintenances [GET]

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        
        {
            "branchId": "000008783",
            "brandName":{"en": "Central RAMA IX", "th": "เซนทรัล พระราม 9"}
            "data": [
                {
                    "id": "b0ee8414",
                    "shopName":"Believe Store Premium",
                    "requestBy":"สมคิด รักงาน",
                    "contanctNumber":"0987767767"
                    "status": "pending",
                    "survey": { "status": false, "createDate": "" }
                    "time": {
                        "requestTime":"12:00-15:00",
                        "startDate": "2020-09-25T08:45:00Z",
                        "endDate": ""
                    },
                    "description": "เปลี่ยนหลอดไฟ",
                    "attachments":[
                        "/maintenance/images/b0ee8414-01.jpg",
                        "/maintenance/images/b0ee8414-02.jpg",
                        "/maintenance/images/b0ee8414-03.jpg"
                    ],
                    "cost":0,
                    "responseBy": {
                        "name": "",
                        "contanctNumber":""
                    },
                    "createDate": "2020-09-25T08:45:00Z"
                },
                {
                    "id": "c0746f59",
                    "shopName":"Suki Shabu Gold",
                    "requestBy":"สมศรี ขยันหมั่นเพียร",
                    "contanctNumber":"0987767000",
                    "status": "in progress",
                    "survey": { "status": false, "createDate": "" }
                    "time": {
                        "requestTime":"9:00-12:00",
                        "startDate": "2020-08-25T08:45:00Z",
                        "endDate": ""
                    },
                    "description": "ไฟรั่ว",
                    "attachments":[],
                    "cost":0,
                    "responseBy": {
                        "name": "มนัส ชำนาญซ่อม",
                        "contanctNumber":"0867777765"
                    },
                    "createDate": "2020-08-25T08:45:00Z"
                },
                {
                    "id": "d0ee8419",
                    "shopName":"Nail Shop",
                    "requestBy":"สมพล มีความเพียร",
                    "contanctNumber":"0987767888"
                    "status": "completed",
                    "survey":  { "status": true, "createDate": "2020-08-30T10:45:00Z" }
                    "time": {
                        "requestTime":"9:00-12:00",
                        "startDate": "2020-08-25T08:45:00Z",
                        "endDate": "2020-08-25T10:00:00Z"
                    },
                    "description": "ซ่อมท่อน้ำรั่ว",
                    "attachments":["/maintenance/images/d0ee8419-01.jpg"],
                    "cost":0,
                    "responseBy": {
                        "name": "มนัส ชำนาญซ่อม",
                        "contanctNumber":"0867777765"
                    },
                    "createDate": "2020-08-25T08:45:00Z"
                }
            ]
        }
        

### Create a New Maintenance [POST]

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
            "shopName":"Suki Shabu Gold",
            "requestBy":"สมศรี ขยันหมั่นเพียร",
            "contanctNumber":"0987767000",
            "status": "in progress",
            "time": {
                "type": "asas",
                "startDate": "2020-08-25T08:45:00Z",
                "endDate": ""
            },
            "description": "ไฟรั่ว",
            "attachments":[]
        }
        
+ Response 201 (application/json)

    + Body

            {
                "result": "Created",
                "id": "c0746f59",
                "shopName":"Suki Shabu Gold",
                "requestBy":"สมศรี ขยันหมั่นเพียร",
                "contanctNumber":"0987767000",
                "status": "in progress",
                "survey": { "status": false, "createDate": "" }
                "time": {
                    "requestTime":"9:00-12:00",
                    "startDate": "2020-08-25T08:45:00Z",
                    "endDate": ""
                },
                "description": "ไฟรั่ว",
                "attachments":[]
                "cost":0,
                "responseBy": {
                    "name": "",
                    "contanctNumber":""
                },
                "createDate": "2020-08-25T08:45:00Z",
                "notificationStatus":false
            }


## Maintenace by Id Collection  [/maintenance/{branchId}/{id}]

### Get Maintenance by Id [GET]

+ Request (application/json)

    + Headers 
     
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        
        {
            "result": "Updated",
            "id": "b0ee8414",
            "shopName":"Believe Store Premium",
            "requestBy":"สมคิด รักงาน",
            "contanctNumber":"0987767767"
            "status": "pending",
            "survey": { "status": false, "createDate": "" }
            "time": {
                "requestTime":"12:00-15:00",
                "startDate": "2020-09-25T08:45:00Z",
                "endDate": ""
            },
            "description": "เปลี่ยนหลอดไฟ",
            "attachments":[
                "/maintenance/images/b0ee8414-01.jpg",
                "/maintenance/images/b0ee8414-02.jpg",
                "/maintenance/images/b0ee8414-03.jpg"
            ],
            "cost":0,
            "responseBy": {
                "name": "",
                "contanctNumber":""
            },
            "createDate": "2020-08-25T08:45:00Z"
        }

### Update Maintenance by Id [PUT]

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
            "shopName":"Suki Shabu Gold",
            "requestBy":"สมศรี ขยันหมั่นเพียร",
            "contanctNumber":"0987767000",
            "status": "completed",
            "time": {
                "requestTime":"15:00-18:00",
                "startDate": "2020-08-25T08:45:00Z",
                "endDate": "2020-08-25T16:00:00Z"
            },
            "description": "ไฟรั่ว ต่อสายดิน เดินสายไฟใหม่",
            "attachments":[],
        }

+ Response 201 (application/json)

    + Body

            {
                "id": "c0746f59",
                "shopName":"Suki Shabu Gold",
                "requestBy":"สมศรี ขยันหมั่นเพียร",
                "contanctNumber":"0987767000",
                "status": "completed",
                "survey": { "status": true, "createDate": "2020-08-30T10:45:00Z" }
                "time": {
                    "requestTime":"15:00-18:00",
                    "startDate": "2020-08-25T08:45:00Z",
                    "endDate": "2020-08-25T16:00:00Z"
                },
                "description": "ไฟรั่ว ต่อสายดิน เดินสายไฟใหม่",
                "attachments":[],
                "cost":550,
                "responseBy": {
                    "name": "มนัส ชำนาญซ่อม
                    "contanctNumber":""
                },
                "notificationStatus":true
                "createDate": "2020-08-25T08:45:00Z"
        
            }

### Delete Maintenance by Id [DELETE] 

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Response 201 (application/json)

    + Body

            {
                "result": "Deleted",
                "id": "c0746f59"
            }
            
            
            
### Rate Maintenance by Id [POST] 
+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
            "q1": 3,
            "q2": 4,
            "q3": 3,
            "q4": 4,
            "q5": 5,
            "description": "เจ้าหน้าที่ดูแลเป็นอย่างดี อาจจะมาสายนิดหน่อย แต่โดยรวมมีความชำนาญ น่าเชื่อถือดี"
        }
        
+ Response 201 (application/json)

    + Body

            {
                "result": "Created",
                "id": "c0746f59",
                "shopName":"Suki Shabu Gold",
                "survey": { "status": true, "createDate": "2020-08-26T10:45:00Z" },
                "notificationStatus": true
                
            }
