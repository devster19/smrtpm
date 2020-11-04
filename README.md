FORMAT: 1A
HOST: https://polls.apiblueprint.org/

# SMARTINVv1.0.2
ตัวอย่าง API Response สำหรับใช้แสดงข้อมูลการชำระเงิน

## คำอธิบาย Response (object)
+ totalAmount: (string) ยอดชำรวมทุก Invoice


+ branchId: 000008783 (string)   ไอดีสาขา

+ brandName: {"en": "Central RAMA IX", "th": "เซนทรัล พระราม 9"}  (object)

    แสดงข้อมูลชื่อภาษา ทั้งไทย และ อังกฤษ
    
+ data: [{}]  (Array of object)

    แสดงข้อมูลที่จำเป็นต่อการแสดงผล  UI ดังต่อไปนี้
    
    **shopId** : (string) ไอดีของร้านที่ทำการแจ้งซ่อม
    
    **invoiceId**: (string) ไอดีใบแจ้งหนี้
    
    **shopName**: (object) ชื่อร้าน
 
    **status**: (string) สถานะการชำระหนี้ประกอบด้วย
    - due
    - overdue
    - due soon (optional)
    
    **paymentDetail**: (object) แสดงข้อสิ่งที่ต้องทำการชำระ
    - total: (string) ยอดชำระทั้งหมดของ Invoice
    - discout: (string) ยอดส่วนลดทั้งหมดของ Invoice
    - vatValue": (string) ยอด VAT
    - taxValue": (string) ยอด TAX
    - paymentItems: : (object of array)
    - id: (string) ไอดีของไอเทมที่ต้องชำระ
    - name: (string) ชื่อรายการที่ต้องชำระ
    - value: (string) ค่าใช้จ่ายแต่ละรายการ
    - description: (object) รายละเอียดเพิ่มเติมที่ต้องการระบุ
        - name: (string) รายละเอียดที่หนึ่งเช่นรอบการชำระ 
        - value: (string) ถ้ามีก็ส่งมายกตัวอย่าง ค่าเช่า จะมียอดเงินของค่า GP มาด้วย ถ้าไม่มีให้คือค่าว่าง ""
    - checked: (boolean) สเตตัสการเลือกสินค้า default = true

+ createDate: (datetime) วันที่ทำการสร้างใบ Invoice
+ endDate: (datetime) วันครบกำหนดชำระ
+ checked: (boolean) สเตตัสการเลือกใบ Invoice default true กรณี stutus = overdue

+ transactionId: (string) ไอดีการชำระ
+ transactionType: (string) ประเภทการชำระ TBC
+ billPayment: (object) ข้อมูลการชำระที่ได้รับจากธนาคาร

    - paymentAmount: (string) ยอดที่ชำระ
    - accountTo: (string) แอคเค้าไอดีที่ชำระTBC
    - ref1: (string) reference ไอดี สำหรับอ้างอิงการชำระเงินกับธนาคาร TBC
    - ref2: (string) reference ไอดี สำหรับอ้างอิงการชำระเงินกับธนาคาร TBC

+ paymentChannel: (string) ธนาคารที่จ่าย
+ paymentMethod: (string) วิธีการชำระ
+ requestBillType: (string) ประเภทการขอบิล
    - include = รวมบิล
    - split = แยกบิล
    
+ requestEmail: (string) อีเมลที่ใช้ในการรับใบแจ้งหนี้
+ requestBillAddress: (string) ที่อยู่จัดส่งบิล
## Invoice Collection [/invoice/]

### List All Invoice(s) [GET]
* แสดงรายการที่จะต้องจ่ายทั้งหมดโดยเรียงลำดับจากรอบบิลที่ใกล้จะถึงรอบจ่ายมากที่สุด
+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        {
            "totalAmount": "796,000.75",
            "data": [ 
                {
                    "invoiceId": "ae76865",
                    "branch": { 
                        "branchId": "b783343", 
                        "nameEN": "Central RAMA IX", 
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId": "s018ee3", 
                        "nameEN": "Beleive Store", 
                        "nameTH": "บีลีฟ สโตร์"
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetail":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "ae76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": {
                                    "name": "อัตราค่าเช่า (GP) Minimum",
                                    "value": "30,000 บาท"
                                },
                                "checked": true
                            },
                            { 
                                "id": "ae76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            },
                            { 
                                "id": "ae76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                               "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            }
                        ]
                    },
                    "createDate": "2019-07-25T08:45:00",
                    "endDate": "2020-07-25T08:45:00",
                    "checked": true
                },
                {
                    "invoiceId": "dd76865",
                    "branch": { 
                        "branchId":"bd22676", 
                        "nameEN": "Central RAMA IX", 
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId":"sd22676", 
                        "nameEN": "Beleive ฺBakery",
                        "nameTH": "บีลีฟ เบเกอรี่"
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetails":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "dd76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": {
                                    "name": "อัตราค่าเช่า (GP) Minimum",
                                    "value": "30,000 บาท"
                                },
                                "checked": true,
                            },
                            { 
                                "id": "dd76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            },
                            { 
                                "id": "dd76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            }
                        ]
                    },
                    "createDate": "2020-01-25T08:45:00",
                    "endDate": "2021-01-25T08:45:00",
                    "checked": false
                },
                {
                    "invoiceId": "dd76865",
                    "branch": { 
                        "branchId": "d345999", 
                        "nameEN": "Central  Bagna", 
                        "nameTH": "เซนทรัล บางนา"
                    },
                    "shop": { 
                        "shopId": "s783343", 
                        "nameEN": "Beleive Electronics", 
                        "nameTH": "บีลีฟ อิเล็กทรอนิกส์"
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetails":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "dd76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": {
                                    "name": "อัตราค่าเช่า (GP) Minimum",
                                    "value": "30,000 บาท"
                                }
                            },
                            { 
                                "id": "dd76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                }
                            },
                            { 
                                "id": "dd76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                }
                            }
                        ]
                    },
                    "createDate": "2019-07-25T08:45:00",
                    "endDate": "2020-07-25T08:45:00",
                    "checked": false
                }
            ]
        }
        
       
        

### Filter and Order Invoices list by BranchId  [POST]
* แสดงรายการบิลที่จะจ่ายโดยมีการกรองข้อมูล
* { filter: null } แสดงรายการทั้งหมดถ้าไม่มีการส่งข้อมูลมา
* { filter: { branches: [], sort: []} } กรองข้อมูลที่จะแสดงจากสาขา หรือ ร้าน หรือทั้งสองเงื่อนไขรวมกัน

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
    
            
+ Request (application/json)

        {
        
            "filter": {
                "branches": ["b783343"],
                "sort": ["duedate"]
            }
                
        }

+ Response 200 (application/json)

        {
            "totalAmount": "796,000.75",
            "data": [ 
                {
                    "invoiceId": "ae76865",
                    "branch": { 
                        "branchId": "b783343", 
                        "nameEN": "Central RAMA IX",
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId": "s018ee3", 
                        "nameEN": "Beleive Store", 
                        "nameTH": "บีลีฟ สโตร์" 
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetails":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "ae76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": {
                                    "name": "อัตราค่าเช่า (GP) Minimum",
                                    "value": "30,000 บาท"
                                },
                                "checked": true
                            },
                            { 
                                "id": "ae76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": "",
                                "checked": true
                            },
                            { 
                                "id": "ae76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": {
                                    "name": "อัตราค่าเช่า (GP) Minimum",
                                    "value": "30,000 บาท"
                                },
                                "checked": true
                            }
                        ]
                    },
                    "createDate": "2019-04-22T08:45:00",
                    "endDate": "2020-04-22T08:45:00",
                    "checked": false
                },
                {
                    "invoiceId": "dd76865",
                    "paymentStatus":false,
                    "branch": { 
                        "branchId": "b783343", 
                        "nameEN": "Central RAMA IX", 
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId": "s783343", 
                        "nameEN": "Beleive Electronics", 
                        "nameTH": "บีลีฟ อิเล็กทรอนิกส์"
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetails":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "dd76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": {
                                    "name": "อัตราค่าเช่า (GP) Minimum",
                                    "value": "30,000 บาท"
                                },
                                "checked": true
                            },
                            { 
                                "id": "dd76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            },
                            { 
                                "id": "dd76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            }
                        ]
                    },
                    "createDate": "2019-07-25T08:45:00",
                    "endDate": "2020-07-25T08:45:00",
                    "checked": false
                }
               
            ]
        }
        
## Make a Payment [/invoice/payment/]

### Create a Single or Multiple Invoice(s) for Payment  [POST]
* ส่วนนี้เป็นการ คาดเดา Header ที่จะใช้ทำการส่ง อาจจะต้องคุยกับทางธนาคารก่อนว่าทำการส่งข้อมูลยังไง แต่จะมีการ ร่าง response เบื้องต้นไว้เพื่อซัพพอร์ตการแสดงผลของ UI

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
            "data":[
            {
                    "invoiceId": "ae76865",
                    "branch": { 
                        "branchId": "b783343", 
                        "nameEN": "Central RAMA IX", 
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId": "s018ee3", 
                        "nameEN": "Beleive Store", 
                        "nameTH": "บีลีฟ สโตร์"
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetails":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "ae76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": {
                                    "name": "อัตราค่าเช่า (GP) Minimum",
                                    "value": "30,000 บาท"
                                },
                                "checked": true
                            },
                            { 
                                "id": "ae76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            },
                            { 
                                "id": "ae76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                },
                                "checked": true
                            }
                        ]
                    },
                    "createDate": "2019-07-25T08:45:00",
                    "endDate": "2020-07-25T08:45:00",
                    "checked": true
                }
            ],
            "paymentChannel":"kbank",
            "paymentMethod": "Internet Banking",
            "requestBillAddress":"shop believe store 9/9 Ratchadaphisek Rd, Huai Khwang, Bangkok 10320"
            "requestBillType":"include",
            "requestEmail":"test@mail.com"
        }
        
+ Response 201 (application/json)

    + Body

            {
                "transactionId": "d7e992f3",
                "transactionType": "PURCHASE",
                "billPayment": {
                    "paymentAmount": "234,763.25",
                    "accountTo": "123456789012345",
                    "ref1": "ae76865"
                },
                "data": [ 
                {
                    "invoiceId": "ae76865",
                    "branch": { 
                        "branchId": "b783343", 
                        "nameEN": "Central RAMA IX", 
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId": "s018ee3", 
                        "nameEN": "Beleive Store", 
                        "nameTH": "บีลีฟ สโตร์"
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetails":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "ae76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                }
                            },
                            { 
                                "id": "ae76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                }
                            },
                            { 
                                "id": "ae76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": {
                                    "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                    "value": ""
                                }
                            }
                        ]
                    },
                    "createDate": "2019-07-25T08:45:00",
                    "endDate": "2020-07-25T08:45:00",
                    "checked": false
                },
                
            ],
            "paymentDate": "2020-07-25T08:45:00",
            "paymentChannel":"kbank",
            "paymentMethod": "Internet Banking",
            "requestBillAddress":"shop believe store 9/9 Ratchadaphisek Rd, Huai Khwang, Bangkok 10320"
            "requestBillType":"include",
            "requestEmail":"test@mail.com"
            }

### Update Payment Item per Invoice [PATCH]
* อัพเดทรายการที่ต้องการจ่ายภายใต้ใบแจ้งหนี้
+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
            "data":[
            {
                    "invoiceId": "ae76865",
                    "branch": { 
                        "branchId": "b783343", 
                        "nameEN": "Central RAMA IX", 
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId": "s018ee3", 
                        "nameEN": "Beleive Store", 
                        "nameTH": "บีลีฟ สโตร์"
                    },
                    "paymentDetails":{
                        "paymentItems":[
                            {
                                "id": "ae76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": "",
                                "checked": true
                            },
                            { 
                                "id": "ae76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": "",
                                "checked": false
                            },
                            { 
                                "id": "ae76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": "",
                                "checked": false
                            }
                        ]
                    }
                    
                }
            ]
        }
        
+ Response 201 (application/json)

    + Body

            {
                "result": "sucessfull"
                "transactionId": "d7e992f3",
                "transactionType": "PURCHASE",
                "billPayment": {
                    "paymentAmount": "200,000.00",
                    "accountTo": "123456789012345",
                    "ref1": "ae76865"
                },
                "data": [ 
                {
                    "invoiceId": "ae76865",
                    "branch": { 
                        "branchId": "b783343", 
                        "nameEN": "Central RAMA IX", 
                        "nameTH": "เซนทรัล พระราม 9"
                    },
                    "shop":  { 
                        "shopId": "s018ee3", 
                        "nameEN": "Beleive Store", 
                        "nameTH": "บีลีฟ สโตร์"
                    },
                    "description": "",
                    "status": "overdue",
                    "paymentDetails":{
                        "total": "234,763.25",
                        "discout": "20,000.00",
                        "vatValue": "2,763.00",
                        "taxValue": "1,190.00",
                        "paymentItems":[
                            {
                                "id": "ae76865-001",
                                "name": "ค่าเช่า",
                                "value": "200,000.00",
                                "description": "",
                                "checked": true
                            },
                            { 
                                "id": "ae76865-002",
                                "name": "ค่าไฟ",
                                "value": "31,345.00", 
                                "description": "",
                                "checked": false
                            },
                            { 
                                "id": "ae76865-003",
                                "name": "ค่าน้ำ",
                                "value": "3,463.25", 
                                "description": "",
                                "checked": false
                            }
                        ]
                    },
                    "createDate": "2019-07-25T08:45:00",
                    "endDate": "2020-07-25T08:45:00",
                    "checked": true
                }
                
            ]
            }
## Payment History [/invoice/payment-history/]
### List All Invoice History [GET]
* แสดงประวัติการชำระใบแจ้งหนี้
+ Request (application/json)

    + Headers 
     
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

            {
                "data" :[
                    {
                        "transactionId": "d7e992f3",
                        "transactionType": "PURCHASE",
                        "billPayment": {
                            "paymentAmount": "796,000.75",
                            "accountTo": "123456789012345",
                            "ref1": "ae76865",
                            "ref2": "dd76865"
                        },
                        "data": [ 
                        {
                            "invoiceId": "ae76865",
                            "branch": { 
                                "branchId": "b783343", 
                                "nameEN": "Central RAMA IX", 
                                "nameTH": "เซนทรัล พระราม 9"
                            },
                            "shop":  { 
                                "shopId": "s018ee3", 
                                "nameEN": "Beleive Store", 
                                "nameTH": "บีลีฟ สโตร์" 
                            },
                            "description": "",
                            "status": "overdue",
                            "paymentDetails":{
                                "total": "234,763.25",
                                "discout": "20,000.00",
                                "vatValue": "2,763.00",
                                "taxValue": "1,190.00",
                                "paymentItems":[
                                    {
                                        "id": "ae76865-001",
                                        "name": "ค่าเช่า",
                                        "value": "200,000.00",
                                        "description": ""
                                    },
                                    { 
                                        "id": "ae76865-002",
                                        "name": "ค่าไฟ",
                                        "value": "31,345.00", 
                                        "description": ""
                                    },
                                    { 
                                        "id": "ae76865-003",
                                        "name": "ค่าน้ำ",
                                        "value": "3,463.25", 
                                        "description": ""
                                    }
                                ]
                            },
                            "createDate": "2019-07-25T08:45:00",
                            "endDate": "2020-07-25T08:45:00",
                            "paymentChannel":"kbank",
                            "paymentMethod": "Internet Banking",
                            "requestBillAddress":"shop believe store 9/9 Ratchadaphisek Rd, Huai Khwang, Bangkok 10320"
                            "requestBillType":"include",
                            "requestEmail":"test@mail.com"
                        },
                        {
                            "invoiceId": "dd76865",
                            "paymentStatus":"paid",
                            "branch": { 
                                "branchId": "b783343", 
                                "nameEN": "Central RAMA IX", 
                                "nameTH": "เซนทรัล พระราม 9"
                            },
                            "shop":  { 
                                "shopId": "s783343", 
                                "nameEN": "Beleive Electronics", 
                                "nameTH": "บีลีฟ อิเล็กทรอนิกส์"
                            },
                            "description": "",
                            "status": "overdue",
                            "paymentDetails":{
                                "total": "234,763.25",
                                "discout": "20,000.00",
                                "vatValue": "2,763.00",
                                "taxValue": "1,190.00",
                                "paymentItems":[
                                    {
                                        "id": "dd76865-001",
                                        "name": "ค่าเช่า",
                                        "value": "200,000.00",
                                       "description": {
                                            "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                            "value": ""
                                        }
                                    },
                                    { 
                                        "id": "dd76865-002",
                                        "name": "ค่าไฟ",
                                        "value": "31,345.00", 
                                        "description": {
                                            "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                            "value": ""
                                        }
                                    },
                                    { 
                                        "id": "dd76865-003",
                                        "name": "ค่าน้ำ",
                                        "value": "3,463.25", 
                                        "description": {
                                            "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                            "value": ""
                                        }
                                    }
                                ]
                            },
                            "createDate": "2019-07-25T08:45:00",
                            "endDate": "2020-07-25T08:45:00",
                        }
                    ],
                    
                    "paymentDate": "2020-07-25T08:45:00",
                    "paymentChannel":"kbank",
                    "paymentMethod": "Internet Banking",
                    "requestBillAddress":"shop believe store 9/9 Ratchadaphisek Rd, Huai Khwang, Bangkok 10320"
                    "requestBillType":"include",
                    "requestEmail":"test@mail.com"
                    
                    },
                    {
                        "transactionId": "a7e992f3",
                        "transactionType": "PURCHASE",
                        "billPayment": {
                            "paymentAmount": "796,000.75",
                            "accountTo": "123456789012345",
                            "ref1": "ae76865",
                            "ref2": "dd76865"
                        },
                        "data": [ 
                        {
                            "invoiceId": "bb3212a2",
                            "branch": { 
                                "branchId": "b783343", 
                                "nameEN": "Central RAMA IX", 
                                "nameTH": "เซนทรัล พระราม 9"
                            },
                            "shop":  { 
                                "shopId": "s018ee3", 
                                "nameEN": "Beleive Store", 
                                "nameTH": "บีลีฟ สโตร์"
                            },
                            "description": "",
                            "status": "overdue",
                            "paymentDetails":{
                                "total": "234,763.25",
                                "discout": "20,000.00",
                                "vatValue": "2,763.00",
                                "taxValue": "1,190.00",
                                "paymentItems":[
                                    {
                                        "id": "ae76865-001",
                                        "name": "ค่าเช่า",
                                        "value": "200,000.00",
                                        "description": ""
                                    },
                                    { 
                                        "id": "ae76865-002",
                                        "name": "ค่าไฟ",
                                        "value": "31,345.00", 
                                        "description": ""
                                    },
                                    { 
                                        "id": "ae76865-003",
                                        "name": "ค่าน้ำ",
                                        "value": "3,463.25", 
                                        "description": ""
                                    }
                                ]
                            },
                            "createDate": "2019-07-25T08:45:00",
                            "endDate": "2020-07-25T08:45:00",
                        }
                        ],
                        "paymentDate": "2020-07-25T08:45:00",
                        "paymentChannel":"kbank",
                        "paymentMethod": "Internet Banking",
                        "requestBillAddress":"shop believe store 9/9 Ratchadaphisek Rd, Huai Khwang, Bangkok 10320"
                        "requestBillType":"include",
                        "requestEmail":"test@mail.com"
                    }
                ]
            }
        

## Download Invoice  [/invoice/payment/{transactionId}]

### Download Invoice Document After Made a Purchase  [GET]
* พาธสำหรับทำการดาวน์โหลดไฟล์ รายการจ่ายใบชำระแจ้งหนี้

+ Request (application/json)

    + Headers 
     
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        
        {
            "transactionId": "a7e992f3",
            "paymentDate": "2020-07-25T08:45:00",
            "downloadPath": "/assets/purchase-a7e992f3.pdf"
        }

## Request Invoice as Document [/invoice/request-invoice/{branchId}/{shopId}]
### List all availalbe invoices for user by shopId  [GET]
* แสดงรายการบิลทั้งหมดที่ที่สามารถให้ลูกค้าทำการขอข้อมูลผ่านอีเมลได้

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        {
            "data":[
                {
                    "year": 2563,
                    "month":[
                        {
                            "name": "Aug",
                            "checked": true,
                            "invoiceLists":[
                                {
                                    "invoiceId": "400000000002320",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "234,763.25",
                                        "discout": "20,000.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        {
                                            "id": "ae76865-001",
                                            "name": "ค่าเช่า",
                                            "value": "200,000.00",
                                            "description": ""
                                        },
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าไฟ",
                                            "value": "31,345.00", 
                                            "description": ""
                                        },
                                        { 
                                            "id": "ae76865-003",
                                            "name": "ค่าน้ำ",
                                            "value": "3,463.25", 
                                            "description": ""
                                        }
                                    ]
                                },
                                {
                                    "invoiceId": "400000000005555",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "31,345.00",
                                        "discout": "00.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าแอร์",
                                            "value": "31,345.00", 
                                            "description": ""
                                        },
                                        
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "year": 2562,
                    "month":[
                        {
                            "name": "Jul",
                            "checked": true,
                            "invoiceLists":[
                                {
                                    "invoiceId": "400000000002320",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "234,763.25",
                                        "discout": "20,000.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        {
                                            "id": "ae76865-001",
                                            "name": "ค่าเช่า",
                                            "value": "200,000.00",
                                            "description": ""
                                        },
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าไฟ",
                                            "value": "31,345.00", 
                                            "description": ""
                                        },
                                        { 
                                            "id": "ae76865-003",
                                            "name": "ค่าน้ำ",
                                            "value": "3,463.25", 
                                            "description": ""
                                        }
                                    ]
                                },
                                {
                                    "invoiceId": "400000000005555",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "31,345.00",
                                        "discout": "00.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าแอร์",
                                            "value": "31,345.00", 
                                            "description": ""
                                        },
                                        
                                    ]
                                }
                            ]
                        },
                        {
                            "name": "Jun",
                            "checked": true,
                            "invoiceLists":[
                                {
                                    "invoiceId": "400000000008888",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "234,763.25",
                                        "discout": "20,000.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        {
                                            "id": "ae76865-001",
                                            "name": "ค่าเช่า",
                                            "value": "200,000.00",
                                            "description": {
                                                "name": "อัตราค่าเช่า (GP) Minimum",
                                                "value": "30,000 บาท"
                                            }
                                        },
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าไฟ",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        { 
                                            "id": "ae76865-003",
                                            "name": "ค่าน้ำ",
                                            "value": "3,463.25", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        }
                                    ]
                                },
                                {
                                    "invoiceId": "400000000005555",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "31,345.00",
                                        "discout": "00.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าแอร์",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
        
        
###Request for Recieved Invoice via Email  [POST]

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
        
            "data": [
                {
                    "year": 2563,
                    "month":[
                        {
                            "name": "Aug",
                            "invoiceLists":["40000000023220", "400000000234444"]
                        },
                        {
                            "name": "Jul",
                            "invoiceLists":["30000000023220"]
                        }
                    ]
                    
                },
                {
                    "year": 2562,
                    "month":[
                        {
                            "name": "Feb",
                            "invoiceLists":["40000000023220", "400000000234444"]
                        },
                        {
                            "name": "Jul",
                            "invoiceLists":["30000000023220"]
                        }
                    ]
                    
                }
            ]
                
        }


+ Response 200 (application/json)

        {
            "status": "successful"
        }


## Request Reciept as Document [/invoice/request-reciept/{branchId}/{shopId}]
### List all availalbe reciepts for user by shopId  [GET]
* แสดงรายการบิลทั้งหมดที่ที่สามารถให้ลูกค้าทำการขอข้อมูลผ่านอีเมลได้
* ฟอแมทกับการเรียกคล้ายกับการขอใบ invoice 
+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9

+ Response 200 (application/json)

        {
            "data":[
                {
                    "year": 2563,
                    "month":[
                        {
                            "name": "Aug",
                            "checked": true,
                            "invoiceLists":[
                                {
                                    "invoiceId": "400000000002320",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "234,763.25",
                                        "discout": "20,000.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    
                                    "paymentItems":[
                                        {
                                            "id": "ae76865-001",
                                            "name": "ค่าเช่า",
                                            "value": "200,000.00",
                                            "description": {
                                                "name": "อัตราค่าเช่า (GP) Minimum",
                                                "value": "30,000 บาท"
                                            }
                                        },
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าไฟ",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        { 
                                            "id": "ae76865-003",
                                            "name": "ค่าน้ำ",
                                            "value": "3,463.25", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        }
                                    ]
                                },
                                {
                                    "invoiceId": "400000000005555",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "31,345.00",
                                        "discout": "00.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าแอร์",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "year": 2562,
                    "month":[
                        {
                            "name": "Jul",
                            "checked": true,
                            "invoiceLists":[
                                {
                                    "invoiceId": "400000000002320",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "234,763.25",
                                        "discout": "20,000.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        {
                                            "id": "ae76865-001",
                                            "name": "ค่าเช่า",
                                            "value": "200,000.00",
                                            "description": {
                                                "name": "อัตราค่าเช่า (GP) Minimum",
                                                "value": "30,000 บาท"
                                            }
                                        },
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าไฟ",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        { 
                                            "id": "ae76865-003",
                                            "name": "ค่าน้ำ",
                                            "value": "3,463.25", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        }
                                    ]
                                },
                                {
                                    "invoiceId": "400000000005555",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "31,345.00",
                                        "discout": "00.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าแอร์",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        
                                    ]
                                }
                            ]
                        },
                        {
                            "name": "Jun",
                            "checked": true,
                            "invoiceLists":[
                                {
                                    "invoiceId": "400000000008888",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "234,763.25",
                                        "discout": "20,000.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        {
                                            "id": "ae76865-001",
                                            "name": "ค่าเช่า",
                                            "value": "200,000.00",
                                            "description": {
                                                "name": "อัตราค่าเช่า (GP) Minimum",
                                                "value": "30,000 บาท"
                                            }
                                        },
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าไฟ",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        { 
                                            "id": "ae76865-003",
                                            "name": "ค่าน้ำ",
                                            "value": "3,463.25", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        }
                                    ]
                                },
                                {
                                    "invoiceId": "400000000005555",
                                    "checked": true,
                                    "paymentDetails":{
                                        "total": "31,345.00",
                                        "discout": "00.00",
                                        "vatValue": "2,763.00",
                                        "taxValue": "1,190.00"
                                    },
                                    "paymentItems":[
                                        { 
                                            "id": "ae76865-002",
                                            "name": "ค่าแอร์",
                                            "value": "31,345.00", 
                                            "description": {
                                                "name": "รอบวันที่ 12 ก.ค. - 14 ส.ค.",
                                                "value": ""
                                            }
                                        },
                                        
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
        
        
###Request for Recieved Invoice via Email  [POST]

+ Request (application/json)

    + Headers 
    
            Authorization: eyJjb250cmFjdElkIjoiMTIzNDU2Nzg5MCJ9
            
+ Request (application/json)

        {
        
            "data": [
                {
                    "year": 2563,
                    "month":[
                        {
                            "name": "Aug",
                            "invoiceLists":["40000000023220", "400000000234444"]
                        },
                        {
                            "name": "Jul",
                            "invoiceLists":["30000000023220"]
                        }
                    ]
                    
                },
                {
                    "year": 2562,
                    "month":[
                        {
                            "name": "Feb",
                            "invoiceLists":["40000000023220", "400000000234444"]
                        },
                        {
                            "name": "Jul",
                            "invoiceLists":["30000000023220"]
                        }
                    ]
                    
                }
            ]
                
        }


+ Response 200 (application/json)

        {
            "status": "successful"
        }
            
