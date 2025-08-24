# Cloud CDN (GSP217)

---

## Task 1: Create and Populate a Cloud Storage Bucket
- Create Cloud Storage bucket: `[your-storage-bucket]`
  - Location type: `Multi-regional`
  - Location: *choose one far from your region*
- Copy sample image:
  ```bash
  gsutil cp gs://cloud-training/gcpnet/cdn/cdn.png gs://[your-storage-bucket]
  ```
- Make bucket public:
  - Grant allUsers → Storage Object Viewer
  - Verify public access to `cdn.png`

## Task 2: Create an HTTP Load Balancer with Cloud CDN
- Navigate: **Network Services → Load Balancing**
- Create new load balancer:
  - Type: `Application Load Balancer (HTTP/HTTPS)`
  - Name: `cdn-lb`

### Backend Configuration
- Create backend bucket: `cdn-bucket`
- Select your storage bucket: `[your-storage-bucket]`
- Enable: **Cloud CDN**
- TTL values:
  - `Client TTL = 1 min`
  - `Default TTL = 1 min`
  - `Maximum TTL = 1 min`

### Frontend Configuration
- Protocol: `HTTP`
- IP version: `IPv4`
- IP address: `Ephemeral`
- Port: `80`

### Finalize
- Review and create load balancer
- Note external IP → `[LB_IP_ADDRESS]`
