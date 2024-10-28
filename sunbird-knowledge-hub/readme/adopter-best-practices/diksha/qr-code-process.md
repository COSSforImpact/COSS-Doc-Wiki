---
icon: elementor
---

# QR Code Process

QR Code Process

Implementation Team

| **Table of Contents**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Load QR Codes 2</strong></p><p>Steps 2</p><p>Details maintained in QRDIAL table 3</p><p><strong>QR Code Delivery 4</strong></p><p>Steps 4</p><p><strong>QR Code Reverse Verification 5</strong></p><p>Steps 5</p><p>Details maintained in QRPACKET table 6</p><p><strong>Other Options 7</strong></p><p>Update Packet Delivery Details 7</p><p>Update a Packet (Add more QR codes) 7</p><p>Move Dial Codes from one packet to another 7</p><p>Retrieve a Packet 7</p><p><strong>QR Report 8</strong></p> |

### **Load QR Codes** <a href="#pr6d58tbktcb" id="pr6d58tbktcb"></a>

![](<../../../../.gitbook/assets/0 (1) (1).png>)

### &#x20;Steps <a href="#s3b4fba3i86y" id="s3b4fba3i86y"></a>

1. Request product team for QR Codes for a state
2. Upon receiving a batch of QR Codes for a state, generate raw images in site - [https://qrexplore.com/generate/](https://qrexplore.com/generate/)
3. Process the raw images using Adobe photoshop and save the processed images
4. Load QR URL, DIAL Code, Raw Image and Processed Image into the QR DIAL Table

### Details maintained in QRDIAL table <a href="#id-77xsx9wbbdpk" id="id-77xsx9wbbdpk"></a>

| **Columns**                          | **Remarks**                                                                                              |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| **DIAL** VARCHAR(10) NOT NULL UNIQUE | DIAL Code shared by product team                                                                         |
| **URL** VARCHAR(180) NOT NULL UNIQUE | QR URL shared by product team                                                                            |
| **RAW\_IMG** BLOB                    | Generated raw image                                                                                      |
| **PRCD\_IMG** BLOB                   | Generated processed image                                                                                |
| **DEL\_FLG** CHAR(1)                 | Delete Flag. Default value is N. Incorporated for future use                                             |
| **R\_CRE\_TIME** DATETIME            | Record Creation Time                                                                                     |
| **RAW\_IMG\_TIME** DATETIME          | Raw Image load time                                                                                      |
| **PRCD\_IMG\_TIME** DATETIME         | Processed Image load time                                                                                |
| **IMG\_EXP\_FLG** CHAR(1)            | Image Exported Flag. Default value is N. When this QR Code goes into a packet, this flag is changed to Y |
| **STATE\_ALLOCATED\_TO** VARCHAR(2)  | Two-Letter State Code to which this QR Code is allocated                                                 |

### **QR Code Delivery** <a href="#wrumg2lbsuf6" id="wrumg2lbsuf6"></a>

![](<../../../../.gitbook/assets/1 (1) (1).png>)

### Steps  <a href="#b1gh4lz5ue91" id="b1gh4lz5ue91"></a>

1. Packet Name - Unique Validation done against existing records in database
2. QR Codes Count - Check whether requested count is available in the database
3. Retrieve the processed images from db and store it in images folder. Update Image Exported Flag as Y for retrieved processed images

(Available dial codes for the state is sorted in ascending order and the requested count is taken from top most records)

1. Packet Name, Dial Codes, Count and Metadata of the packet(book) shared by the state are captured in the database in the QRPACKET table
2. Tracker xls is created
3. ZIP file is created with Images folder and Tracker xls - **SerialNo-PacketName.ZIP**\
   Sample Packet - [1 - GUJ\_GARVI\_STD\_8.zip](https://drive.google.com/open?id=1oa8s4ZTWgbJuuRlCc2aSBoFCTS0c7lun)

### **QR Code Reverse Verification** <a href="#ihsx2mkeb7aw" id="ihsx2mkeb7aw"></a>

![](<../../../../.gitbook/assets/2 (1) (1).png>)

### Steps <a href="#dwkgujog1mwg" id="dwkgujog1mwg"></a>

1. All images are extracted from the shared pdfs using Adobe Acrobat Pro DC
2. All QR codes are read from the extracted images using ZXing Java library
3. Extracted QR Codes are reverse verified against the data(Actual allocated QR codes, count) present in the database for that particular packet.
4. Reverse Verification details are updated in the QRPACKET table for the given packet

### Details maintained in QRPACKET table <a href="#wndji51ckj7i" id="wndji51ckj7i"></a>

| **QR Code Delivery as Packets**            |                                                                                                                   |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| **PKT\_NAME** VARCHAR(80) NOT NULL UNIQUE, | Packet Name given by state team                                                                                   |
| **DIAL\_LIST** VARCHAR(8000) NOT NULL,     | Dial Codes allocated to the packet (concatenated by pipe symbol)                                                  |
| **COUNT** INT,                             | Number of dial codes allocated to the packet                                                                      |
| **CREATED\_FOR** VARCHAR(80),              | State code                                                                                                        |
| **MEDIUM** VARCHAR(80),                    | Metadata of the packet/book - Lanuage Medium of the book                                                          |
| **GRADE** VARCHAR(20),                     | Metadata of the packet/book - Grade/Class of the book                                                             |
| **PO** VARCHAR(180),                       | Metadata of the packet/book - Project Officer for this book                                                       |
| **AST\_PO** VARCHAR(180),                  | Metadata of the packet/book - Asst. Project Officer for this book                                                 |
| **DEL\_FLG** CHAR(1),                      | Delete Flag. Default value is N. Incorporated for future use.                                                     |
| **R\_CRE\_TIME** DATETIME,                 | Record Creation Time                                                                                              |
| **Update Packet Delivery Details**         |                                                                                                                   |
| **PKT\_SENT\_ON** DATETIME,                | Packet Delivery Date                                                                                              |
| **PKT\_SENT\_TO** VARCHAR(180),            | Packet Delivered To - Name or Email Id                                                                            |
| **PKT\_SENT\_FLG** CHAR(1),                | Packet Sent Flag. Default value is N. When packet is delivered, it will be changed to Y                           |
| **QR Code Reverse Verification**           |                                                                                                                   |
| **REVERSE\_VERIFIED\_FLG** CHAR(1),        | Reverse Verified Flag. Default value is N. It will be changed to Y after first reverse verification of the packet |
| **REVERSE\_VERIFIED\_ON** DATETIME,        | Last reverse verification time                                                                                    |
| **USED\_COUNT** INT,                       | Number of QR Codes actually used in the book **Eg.** **2**                                                        |
| **USED\_CODES** VARCHAR(8000),             | Actually used dial codes - Pipe separated **Eg. 123QWE\|GAWE45\|**                                                |
| **UNUSED\_COUNT** INT,                     | Number of Unused QR codes from allocated count **Eg.** **2**                                                      |
| **UNUSED\_CODES** VARCHAR(8000),           | Unused dial codes - Pipe separated **Eg. 123QWE\|GAWE45\|**                                                       |
| **ADDITIONAL\_USED\_COUNT** INT,           | Number of additional used QR codes from other packets **Eg.** **2**                                               |
| **ADDITIONAL\_USED\_CODES** VARCHAR(8000), | Additional dial codes from other packets - Pipe Separated **Eg. 123QWE\|GAWE45\|**                                |
| **ADDITIONAL\_USED\_FROM** VARCHAR(8000),  | Packet from which additional codes are taken from **Eg. OTHERPACKETNAME=DIAL1\|DIAL2;**                           |
| **DUP\_COUNT** INT,                        | Number of codes allocated within this packet that are used more than once **Eg. 2**                               |
| **DUP\_CODES** VARCHAR(8000),              | Duplicated Codes - Pipe separated **Eg. 123QWE\|GAWE45\|**                                                        |

### Other Options <a href="#d0e1j66hlfd5" id="d0e1j66hlfd5"></a>

### Update Packet Delivery Details <a href="#id-5yqj4xl08m2i" id="id-5yqj4xl08m2i"></a>

**Input** - Packet Sent Date, Packet Sent To, Packet Name

**Process** - Packet Sent Date and Packet Sent To details will be updated in the QRPACKET table

**Output** - Confirmation Message

### Update a Packet (Add more QR codes) <a href="#z31emdypx251" id="z31emdypx251"></a>

For an existing packet, more QR codes can be generated

**Input** - Packet Name, Extra QR Codes count

**Validation** - Check whether packet name exists in QRPACKET table, Check whether requested number of QR codes are available in QRDIAL table

**Process** - Update the QRPACKET, QRDIAL records and retrieve extra codes - processed images - from database

**Output** - Zip file having extra qr code images and tracker xlsx file

### Move Dial Codes from one packet to another <a href="#b9t4kwjkzy4d" id="b9t4kwjkzy4d"></a>

**Input** - from packet name, to packet name, dial codes

**Process** - Move dial codes from one packet to another. Update records for both packets in QRPACKET table

**Ouptut** - Confirmation message

### Retrieve a Packet <a href="#id-855ce29ih27q" id="id-855ce29ih27q"></a>

**Input** - Packet Name to be retrieved

**Process** - Fetches processed image files for the given packet from the database

**Output** - Zip file having qr code image files and tracker xlsx file

**There’s a QR\_PACKET\_HISTORY table. Before changing any record in QRPACKET table, the record is backed up in the QR\_PACKET\_HISTORY table with the backup date/time**

### QR Report <a href="#jw4qyrfq4tm0" id="jw4qyrfq4tm0"></a>

Three tables are maintained for reporting purposes

**QR\_POC** - Point of contact for each state is maintained here

**QR\_REPORT** - Table having report data

**QR\_REPORT\_HISTORY** - Table having report history data

A stored procedure(**GEN\_QR\_RPT**) is created for reporting purpose. When this stored procedure is called, it collects all the relevant data for reporting from **QRPACKET** table and populates **QR\_REPORT** table. The whole data of **QR\_REPORT** table is exported as CSV and shared as report

**Sample Report**

| **State**             | **QR Codes Delivery** | **QR Codes Reverse Verification** | **POC**                           |                               |                        |                                                           |                     |                                                                         |                               |       |                                |
| --------------------- | --------------------- | --------------------------------- | --------------------------------- | ----------------------------- | ---------------------- | --------------------------------------------------------- | ------------------- | ----------------------------------------------------------------------- | ----------------------------- | ----- | ------------------------------ |
| **Packets Requested** | **Packets Delivered** | **QR Codes Delivered**            | **Reverse Verification Requests** | **Reverse Verification done** | **Allocated QR Codes** | <p><strong>Used</strong><br><strong>QR Codes</strong></p> | **Unused QR Codes** | <p><strong>Additional Used</strong></p><p><strong>QR Codes</strong></p> | **Packets having duplicates** |       |                                |
| AP                    | 37                    | 37                                | 6320                              | 36                            | 36                     | 5902                                                      | 3854                | 2052                                                                    | 4                             | 0     | Alia Ali/Paluru Abhign Sai     |
| MH                    | 555                   | 555                               | 13754                             | 496                           | 496                    | 11720                                                     | 11707               | 2701                                                                    | 2688                          | 0     | Rakesh Kumar Jha/Ikpreet Singh |
| RJ                    | 5                     | 5                                 | 500                               | 2                             | 1                      | 66                                                        | 66                  | 0                                                                       | 0                             | 0     | Mahesh Pakalapati              |
| TN                    | 54                    | 54                                | 2415                              | 0                             | 0                      | 0                                                         | 0                   | 0                                                                       | 0                             | 0     | Monica Shivakumar              |
| UP                    | 91                    | 91                                | 1928                              | 0                             | 0                      | 0                                                         | 0                   | 0                                                                       | 0                             | 0     |                                |
| **Total**             | **742**               | **742**                           | **24917**                         | **533**                       | **533**                | **17688**                                                 | **15627**           | **4753**                                                                | **2692**                      | **0** |                                |
