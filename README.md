# Install Node-red by docker-compose
**Node-RED** คือเครื่องมือพัฒนาโปรแกรมแบบ Low-code หรือ Visual Programming ด้วยการลากและวาง (Drag-and-Drop) สร้างชุดคำสั่งเป็นภาพ (Flow-based programming) พัฒนาโดย IBM บนพื้นฐานของ Node.js ใช้สำหรับเชื่อมต่ออุปกรณ์ฮาร์ดแวร์, ระบบ IoT, API และบริการออนไลน์ต่างๆ เข้าด้วยกันอย่างรวดเร็ว

## Getting started
Application ที่ต้องมี

[Install docker version ต่างๆ เข้าไปดูได้ที่นี้ ](https://www.docker.com/get-started/)
[Git Version control](https://git-scm.com/install/)
```bash
git clone https://github.com/manaprae/node-red.git
cd node-red
```
เริ่มต้นทำงาน ด้วยคำสั่ง
```bash
docker compose up

[+] up 20/20
 ✔ Image nodered/node-red Pulled                                                       12.4s
 ✔ Container node-red     Created                                                       0.7s
Attaching to node-red
node-red  | 28 Aug 14:29:00 - [info]
node-red  | 
node-red  | Welcome to Node-RED
node-red  | ===================
node-red  | 
node-red  | 28 Aug 14:29:00 - [info] Node-RED version: v5.0.4
node-red  | 28 Aug 14:29:00 - [info] Node.js  version: v24.18.1
node-red  | 28 Aug 14:29:00 - [info] Linux 6.6.87.2-microsoft-standard-WSL2 x64 LE
node-red  | 28 Aug 14:29:00 - [info] Loading palette nodes
node-red  | 28 Aug 14:29:00 - [info] Settings file  : /data/settings.js
node-red  | 28 Aug 14:29:00 - [info] Context store  : 'default' [module=memory]
node-red  | 28 Aug 14:29:00 - [info] User directory : /data
node-red  | 28 Aug 14:29:00 - [warn] Projects disabled : editorTheme.projects.enabled=false
node-red  | 28 Aug 14:29:00 - [info] Flows file     : /data/flows.json
node-red  | 28 Aug 14:29:00 - [info] Creating new flow file
node-red  | 28 Aug 14:29:00 - [warn]
node-red  | 
node-red  | ---------------------------------------------------------------------
node-red  | Your flow credentials file is encrypted using a system-generated key.
node-red  | 
node-red  | If the system-generated key is lost for any reason, your credentials
node-red  | file will not be recoverable, you will have to delete it and re-enter
node-red  | your credentials.
node-red  | 
node-red  | You should set your own key using the 'credentialSecret' option in
node-red  | your settings file. Node-RED will then re-encrypt your credentials
node-red  | file using your chosen key the next time you deploy a change.
node-red  | ---------------------------------------------------------------------
node-red  | 
node-red  | 28 Aug 14:29:00 - [info] Server now running at http://127.0.0.1:1880/
node-red  | 28 Aug 14:29:00 - [warn] Encrypted credentials not found
node-red  | 28 Aug 14:29:00 - [info] Starting flows
node-red  | 28 Aug 14:29:00 - [info] Started flows
```
ทดสอบเข้าด้วยการเปิด web browser ผ่าน http://127.0.0.1:1880/

![์nodered](https://github.com/manaprae/node-red/blob/main/1787904747686.jpg)

แต่ระบบยังไม่มี แต่ยังไม่มี Authentication

```bash
docker-compose up -d
docker exec -it node-red /bin/bash
b998d01444e1:/usr/src/node-red#
```
จะเข้าสู่ container แล้วใช้คำลั่งสร้าง password
```bash
node-red-admin hash-pw
Password: <copy-password-encryp>
```
แล้วเอาไปใส่ใน settings.js
```bash
vi /data/settings.js
```
ค้นหาบรรทัดนี้ ที่ ขึ้นต้นด้วย adminAuth: { 
แล้วแก้ไขตามนี้
```    adminAuth: {
        type: "credentials",
        users: [{
            username: "admin",
            password: "<paste-password-encryp>",
            permissions: "*"
        }]
    },
```
save แล้ว exit
ออกมาจาก container
แล้วสั่ง

```bash
docker compose restart
```
![login](https://github.com/manaprae/node-red/blob/main/1787902689653.jpg)

