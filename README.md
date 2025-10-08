# GCP VPC Peering (Cross-Project) using Google Cloud Console (GUI)

This guide walks you through setting up **VPC Network Peering between two different GCP projects** using the **Google Cloud Console (GUI)** — no command-line tools required.

---

## 📌 Use Case

Establish a **private connection** between services running in separate GCP projects using VPC peering. This allows secure communication over internal IPs without exposing traffic to the internet.

---

## 🧭 High-Level Architecture

```

Project A (VPC-A)                     Project B (VPC-B)
+------------------+                 +------------------+
|  Subnet A        | <-- Peering --> |  Subnet B        |
|  VM, GKE, etc.   |                 |  VM, GKE, etc.   |
+------------------+                 +------------------+

```

---

## 🧑‍💻 Prerequisites

- Two GCP projects with billing enabled
- VPC networks created in each project (non-overlapping IP ranges)
- IAM roles:
  - **Network Admin** in both projects
  - Optional: **Project Editor/Owner**

---

## ✅ Steps (Using GCP Console)

### Step 1: Go to the VPC Network Page

1. Navigate to the **VPC Network** section in **Project A**:
   - https://console.cloud.google.com/networking/networks

2. Click on your VPC network (e.g., `vpc-a`).

---

### Step 2: Create Peering from Project A to Project B

1. Click the **"Peerings"** tab.
2. Click **"Create Peering Connection"**.
3. Fill in the fields:
   - **Name**: `peering-to-b`
   - **Your VPC network**: `vpc-a`
   - **Peer project ID**: `PROJECT_B_ID`
   - **Peer VPC network name**: `vpc-b`
4. Enable **Exchange custom routes** if needed.
5. Click **Create**.

> Note: Peering is **not active** until both sides have configured it.

---

### Step 3: Repeat in Project B

1. Switch to **Project B** in the Console.
2. Go to **VPC Network → Networks**.
3. Select your VPC (e.g., `vpc-b`) → **Peerings** → **Create Peering Connection**.
4. Enter:
   - **Name**: `peering-to-a`
   - **Your VPC network**: `vpc-b`
   - **Peer project ID**: `PROJECT_A_ID`
   - **Peer VPC network name**: `vpc-a`
5. Enable **Exchange custom routes** if needed.
6. Click **Create**.

---

### Step 4: Verify Peering Status

- In both projects, go to the **Peerings** tab of your VPC.
- Status should show as **"ACTIVE"**.
- If it's "INACTIVE", double-check names, project IDs, and permissions.

---

## 🔐 Permissions Required

| Role              | Description                         |
|-------------------|-------------------------------------|
| Network Admin     | Required to create/manage VPCs      |
| Project Viewer    | Optional; to view VPC configurations|
| Compute Admin     | To manage routes (if needed)        |

---

## 🚧 Considerations

- **IP ranges must not overlap.**
- **Peering is NOT transitive** (A ↔ B, B ↔ C ≠ A ↔ C).
- You cannot use IAM-based access control across peered networks.
- Ensure firewall rules allow traffic between subnets.

---

## 📚 References

- [VPC Network Peering Overview](https://cloud.google.com/vpc/docs/vpc-peering)
- [Peering via Console](https://cloud.google.com/vpc/docs/using-vpc-peering#console)

---


Would you like to include **screenshots** or a **troubleshooting guide** for common issues like "inactive peering" or "firewall blocking traffic"?
