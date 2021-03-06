FORMAT: 1A
HOST: https://polls.apiblueprint.org/

# Maintenance

ตัวอย่างออกแบบ API สำหรับงานแจ้งซ่อม



## คำอธิบาย Response (object)
+ branchId: 000008783 (string)

    ตัวอย่าง  ไอดีสาขา.

+ brandName: {"en": "Central RAMA IX", "th": "เซนทรัล พระราม 9"}  (object)

    แสดงข้อมูลชื่อภาษา ทั้งไทย และ อังกฤษ
    
+ data: [{}]  (Array of object)

    แสดงข้อมูลที่จำเป็นต่อการแสดงผล  UI ดังต่อไปนี้
    
    **shopId** : (string) ไอดีของร้านที่ทำการแจ้งซ่อม
    
    **shopName**: (object) ชื่อร้าน
    
    **requestBy**: (string) ชื่อผู้แจ้งซ่อม

    **contanctNumber**: (string) เบอร์โทรผู้แจ้งซ่อม
    
    **survey**: (object) แสดงสถานะประเมินการแจ้งซ่อม
    - default = false , true เมื่อมีการประเมินแล้ว
    - createDate:(datetime)  วันที่ทำการประเมิน

    **time**: (object) แสดงวันทำรายการ
    - *requestTime*: (string) แสดงช่วงเวลาที่ต้องการให้ช่างเข้าไปดำเนินการซ่อม
    - *startDate*: (datetime) วันเริ่มดำเนินการแจ้งซ่อม
    - *endDate*: (datetime)  วันสิ้นสุดงาน
    
    **type**: (object) ประเภทของงานแจ้งซ่อม
        - *category*: (string) หัวข้อการแจ้งซ่อมยึดตามระบบที่มีปัจจุบัน
        - *subcategory*: (string) รายละเอียดย่อยการแจ้งซ่อมที่สัมพันธ์กับหัวข้อการแจ้ง ยึดตามข้อมูลปัจจุบัน
        
    **description**: (string) รายละเอียดเพิ่มเติมการแจ้งซ่อม
    
    **attachments**: (array of string) พาธรูปที่ผู้ใช้อัพโหลด ประกอบการแจ้งซ่อม
    
    **cost**: (number) ค่าใช้จ่ายในการซ่อม
     
    **status**: (string) สถานะล่าสุดของการซ่อม
    
    **responseBy**: (object) รายละเอียดของช่าง
    - name: (string) ชื่อของช่างซ่อม
    - contactNumber: (string) เบอร์โทรติดต่อช่าง
    
    **createDate**: (datetime) วันและเวลาที่สร้างรายการแจ้งซ่อม
    
    **updateDate**: (datetime) วันและเวลาที่มีการอัพเดทรายการแจ้งซ่อม
    
    **updateBy**: (string) ชื่อผู้ทำการอัพเดทข้อมูล
     
     

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
                        "startDate": "2020-09-25T00:00:00",
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
                    "updateDate": null,
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
                    "updateDate": null,
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
            "type": {"category":"EXISTING_CATEGORY", "subcategory":"EXISTING_RELATED_SUBCATEGORY"},
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
                "updateDate": null,
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
                    "updateDate": null,
                    "updateBy": ""
                }
            ]
        }

### Update Maintenance by ShopId [PUT]
* อัพเดทดูรายละเอียดการแจ้งซ่อมทีละรายการ
+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)
    

        
            {
               "id": "c0746f59",
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
                "data": [
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
                        "updateDate": null,
                        "updateBy": ""
                    }
                ]
                
            }


            
            
### Rate Maintenance by ShopId [POST] 
* ประเมินการแจ้งซ่อม
+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
            "id": "c0746f59",
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
                "shopName":"Suki Shabu Gold",
                "survey": { "status": true, "createDate": "2020-08-26T10:45:00" }
            }
            

            



