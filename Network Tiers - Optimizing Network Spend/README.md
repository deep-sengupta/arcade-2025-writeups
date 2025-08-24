# Network Tiers – Optimizing Network Spend

---

## Task 1: Create the VM Instances

### Create Premium Tier VM
- Go to **Compute Engine → VM Instances**
- Click **Create Instance**
- Set properties:
  - Name: `vm-premium`
  - Region: `[your-region]`
  - Zone: `[your-zone]`
  - Series: `E2`
  - Machine type: `e2-medium (2 vCPU)`
- Click **Networking → default network**
  - Verify **Network Service Tier = Premium** (default)
- Click **Done**, then **Create**

### Create Standard Tier VM
- Go to **Compute Engine → VM Instances**
- Click **Create Instance**
- Set properties:
  - Name: `vm-standard`
  - Region: `[your-region]`
  - Zone: `[your-zone]`
  - Series: `E2`
  - Machine type: `e2-medium (2 vCPU)`
- Click **Networking → default network**
  - Change **Network Service Tier = Standard**
- Click **Done**, then **Create**

## Notes
- Both VMs:
  - Same machine type, region, zone, and VPC network
  - Only difference = **Network Service Tier**
- Record external IP addresses:
  - Premium VM IP → `[premium-IP]`
  - Standard VM IP → `[standard-IP]`
