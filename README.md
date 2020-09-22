FORMAT: 1A
HOST: https://polls.apiblueprint.org/

# Maintenance

ตัวอย่างออกแบบ API สำหรับงานแจ้งซ่อม


## Maintenance by Branch Collection  [/maintenance/{branchId}]

### List All Maintenances [GET]
* ทำหน้าที่แสดงผลรายการแจ้งซ่อมทั้งหมด:

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        
        {
            "branchId": "000008783",
            "brandName":{"en": "Central RAMA IX", "th": "เซนทรัล พระราม 9"}
            "data": [
                {
                    "shopId": "b0ee8414",
                    "shopName":"Believe Store Premium",
                    "requestBy":"สมคิด รักงาน",
                    "contanctNumber":"0987767767",
                    "survey": { "status": false, "createDate": "" },
                    "time": {
                        "requestTime":"12:00-15:00",
                        "startDate": "2020-09-25T08:45:00",
                        "endDate": ""
                    },
                    "type": "EXISTING_MR_TYPE",
                    "description": "ไฟรั่ว",
                    "attachments":[
                        "/maintenance/images/b0ee8414-01.jpg",
                        "/maintenance/images/b0ee8414-02.jpg",
                        "/maintenance/images/b0ee8414-03.jpg"
                    ],
                    "cost":0,
                    "status":"pending",
                    "responseBy": {
                        "name": "มนัส ชำนาญซ่อม",
                        "contanctNumber":"0867777765",
                        "responseMessage":""
                    },
                    "createDate": "2020-09-25T08:45:00",
                    "updateDate": "",
                    "updateBy": ""
                },
                {
                    "shopId": "c0746f59",
                    "shopName":"Suki Shabu Gold",
                    "requestBy":"สมศรี ขยันหมั่นเพียร",
                    "contanctNumber":"0987767000",
                    "status": "in progress",
                    "survey": { "status": false, "createDate": "" }
                    "time": {
                        "requestTime":"9:00-12:00",
                        "startDate": "2020-08-25T08:45:00",
                        "endDate": ""
                    },
                   "type": "other",
                    "description": "ไฟรั่วและมีอาการกระพริบติดๆ ดับๆ ตลอดเวลา",
                    "attachments":[
                        "/maintenance/images/b0ee8414-01.jpg",
                        "/maintenance/images/b0ee8414-02.jpg",
                        "/maintenance/images/b0ee8414-03.jpg"
                    ],
                    "attachments":[],
                    "cost":0,
                    "responseBy": {
                        "name": "มนัส ชำนาญซ่อม",
                        "contanctNumber":"0867777765"
                    },
                    "createDate": "2020-08-25T08:45:00",
                    "createDate": "2020-08-25T08:45:00",
                    "updateDate": "",
                    "updateBy": ""
                }
            ]
        }
        

### Create a New Maintenance [POST]
* เปิดงานแจ้งซ่อมใหม่

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
            "shopId":"bb00232",
            "shopName":"Suki Shabu Gold",
            "requestBy":"สมศรี ขยันหมั่นเพียร",
            "contanctNumber":"0987767000",
            "status": "in progress",
            "time": {
                "requestTime":"9:00-12:00",
                "startDate": "2020-08-25T08:45:00",
                "endDate": ""
            },
            "type": "EXISTING_MR_TYPE",
            "description": "ไฟรั่ว",
            "attachments":[]
        }
        
+ Response 201 (application/json)

    + Body

            {
                "result": "Created",
                "jobId": "c0746f59",
                "shopName":"Suki Shabu Gold",
                "requestBy":"สมศรี ขยันหมั่นเพียร",
                "contanctNumber":"0987767000",
                "status": "in progress",
                "survey": { "status": false, "createDate": "" },
                "time": {
                    "requestTime":"9:00-12:00",
                    "startDate": "2020-08-25T08:45:00",
                    "endDate": ""
                },
                "type": "EXISTING_MR_TYPE",
                "description": "ไฟรั่ว",
                "attachments":[]
                "cost":0,
                "responseBy": {
                    "name": "",
                    "contanctNumber":"",
                    "responseMessage":""
                },
                "createDate": "2020-08-25T08:45:00",
                "updateDate": "",
                "updateBy": ""
            }


## Maintenace by ShopId Collection  [/maintenance/{branchId}/{shopId}]

### Get Maintenance by ShopId [GET]
* ดูรายละเอียดการแจ้งซ่อมทีละรายการ
+ Request (application/json)

    + Headers 
     
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        
        {
            "id": "b0ee8414",
            "shopName":"Believe Store Premium",
            "requestBy":"สมคิด รักงาน",
            "contanctNumber":"0987767767"
            "status": "pending",
            "survey": { "status": false, "createDate": "" }
            "time": {
                "requestTime":"12:00-15:00",
                "startDate": "2020-09-25T08:45:00",
                "endDate": ""
            },
            "type": "EXISTING_MR_TYPE",
            "description": "ไฟรั่ว"",
            "attachments":[
                "/maintenance/images/b0ee8414-01.jpg",
                "/maintenance/images/b0ee8414-02.jpg",
                "/maintenance/images/b0ee8414-03.jpg"
            ],
            "cost":0,
            "responseBy": {
                "name": "",
                "contanctNumber":"",
                "responseMessage":""
            },
            "createDate": "2020-08-25T08:45:00",
            "updateDate": "",
            "updateBy": ""
        }

### Update Maintenance by ShopId [PUT]
* อัพเดทดูรายละเอียดการแจ้งซ่อมทีละรายการ
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
                "startDate": "2020-08-25T08:45:00",
                "endDate": "2020-08-25T16:00:00"
            },
            "type": "EXISTING_MR_TYPE",
            "description": "ไฟรั่ว",
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
                "survey": { "status": true, "createDate": "2020-08-30T10:45:00" }
                "time": {
                    "requestTime":"15:00-18:00",
                    "startDate": "2020-08-25T08:45:00",
                    "endDate": "2020-08-25T16:00:00"
                },
                "type": "EXISTING_MR_TYPE",
                "description": "ไฟรั่ว"",
                "attachments":[],
                "cost":550,
                "responseBy": {
                    "name": "มนัส ชำนาญซ่อม,
                    "contanctNumber":"",
                    "responseMessage":""
                },
                "createDate": "2020-08-25T08:45:00",
                "updateDate": "",
                "updateBy": ""
            }

### Delete Maintenance by ShopId [DELETE] 
* ลบการแจ้งซ่อมทีละรายการ
+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Response 201 (application/json)

    + Body

            {
                "result": "Deleted",
                "id": "c0746f59"
            }
            
            
            
### Rate Maintenance by ShopId [POST] 
* ประเมินการแจ้งซ่อม
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
                "survey": { "status": true, "createDate": "2020-08-26T10:45:00" }
            }
            
## Maintenace for Operator Collection  [/maintenance/getmaintenance/]

### Get All My Tasks [POST] 
* ดูรายการงานทั้งหมดของช่าง

+ Request (application/json)

        {
            "username": "",
            "password": ""
        }
        
+ Response 201 (application/json)

    + Body

            {
               "data":[
                    {
                        "id": "b0ee8414",
                        "branchId": "000008783",
                        "brandName":{"en": "Central RAMA IX", "th": "เซนทรัล พระราม 9"},
                        "shopName":"Believe Store Premium",
                        "requestBy":"สมคิด รักงาน",
                        "contanctNumber":"0987767767",
                        "survey": { "status": false, "createDate": "" }
                        "time": {
                            "requestTime":"12:00-15:00",
                            "startDate": "2020-09-25T08:45:00",
                            "endDate": ""
                        },
                        "description": "เปลี่ยนหลอดไฟ",
                        "attachments":[
                            "/maintenance/images/b0ee8414-01.jpg",
                            "/maintenance/images/b0ee8414-02.jpg",
                            "/maintenance/images/b0ee8414-03.jpg"
                        ],
                        "cost":0,
                        "status":"pending",
                        "responseBy": {
                            "name": "มนัส ชำนาญซ่อม",
                            "contanctNumber":"0867777765",
                            "responseMessage":""
                        },
                        "createDate": "2020-09-25T08:45:00",
                        "updateDate": "",
                        "updateBy": ""
                    }
               ]
            }
