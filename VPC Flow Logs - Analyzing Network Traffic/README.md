# VPC Flow Logs - Analyzing Network Traffic (GSP212)

https://github.com/user-attachments/assets/4602e884-cb11-4948-adc3-970266f1f926

---

## Task 1: Configure a Custom Network with VPC Flow Logs
- Create VPC network: `vpc-net`
- Subnet: `vpc-subnet` (10.1.3.0/24) with Flow Logs enabled
- Firewall rule: `allow-http-ssh` → tcp:80, tcp:22


## Task 2: Create an Apache Web Server
- VM name: `web-server`
- Series: `E2`, Type: `e2-micro`
- Firewall: Allow HTTP
- Network: `vpc-net`, Subnet: `vpc-subnet`
- Install Apache2:
  ```bash
  sudo apt-get update
  sudo apt-get install apache2 -y
  echo '<!doctype html><html><body><h1>Hello World!</h1></body></html>' | sudo tee /var/www/html/index.html
  exit
  ```

## Task 3: Verify Network Traffic Logging
- Access web server via external IP  
- Find client IP  
- Logs: `compute.googleapis.com/vpc_flows`  
- Check fields:  
  - Source IP/Port  
  - Destination IP/Port  
  - Protocol  
  - Bytes sent  

## Task 4: Export Network Traffic to BigQuery
- Create sink: `vpc-flows`
- Destination dataset: `bq_vpc_flows`
- Generate traffic:
  ```bash
  export MY_SERVER=<EXTERNAL_IP>
  for ((i=1;i<=50;i++)); do curl $MY_SERVER; done
  ```

- Dataset: `bq_vpc_flows`
- Query:
  ```sql
  #standardSQL
  SELECT
    jsonPayload.src_vpc.vpc_name,
    SUM(CAST(jsonPayload.bytes_sent AS INT64)) AS bytes,
    jsonPayload.src_vpc.subnetwork_name,
    jsonPayload.connection.src_ip,
    jsonPayload.connection.src_port,
    jsonPayload.connection.dest_ip,
    jsonPayload.connection.dest_port,
    jsonPayload.connection.protocol
  FROM
    `your_table_id`
  GROUP BY
    jsonPayload.src_vpc.vpc_name,
    jsonPayload.src_vpc.subnetwork_name,
    jsonPayload.connection.src_ip,
    jsonPayload.connection.src_port,
    jsonPayload.connection.dest_ip,
    jsonPayload.connection.dest_port,
    jsonPayload.connection.protocol
  ORDER BY
    bytes DESC
  LIMIT 15;
  ```
