# ลำดับขั้นการรัน Docker

## 1.  สร้างไฟล์ docker-compose.yml
คัดลอกมาจากใบงานที่ 7

``` yaml
services:
  esp32-dev:
    image: espressif/idf:latest
    container_name: esp32-lab8
    volumes:
      - .:/project
    working_dir: /project
    tty: true
    stdin_open: true
    environment:
      - IDF_PATH=/opt/esp/idf
    command: /bin/bash
    networks:
      - esp32-network

networks:
  esp32-network:
    driver: bridge
```

2. run docker

``` bash
docker-compose up -d

```


3. ตรวจสอบชื่อ service เพื่อที่จะเข้าไปใช้ bash ใน  docker
``` bash
docker-compose ps -a

```

ควรจะได้ชื่อ service เป็น esp32-dev ตามที่ใส่ในไฟล์ docker-compose.yml


4. เชื่อมต่อเข้าไปใช้ bash shell ใน docker
``` bash
docker-compose exec -it esp32-dev bash
```

5. Export environment สำหรับการพัฒนา ESP32

``` bash
  . $IDF_PATH/export.sh
```

