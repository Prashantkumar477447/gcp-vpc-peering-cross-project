# GCP VPC Peering Across Projects

This repository provides step-by-step instructions and Terraform/IaC templates (if needed) for setting up **VPC Network Peering between two different Google Cloud Platform (GCP) projects**.

## 📌 Overview

VPC Network Peering allows private connectivity across two Virtual Private Cloud (VPC) networks in GCP. This setup enables secure and high-performance internal traffic between resources in two separate GCP projects, without traversing the public internet.

### 🔗 Key Use Case

- Internal communication between services hosted in **Project A** and **Project B**.
- Centralized networking (shared VPC model alternative).
- Hybrid architectures and service segregation by project.

---

## 🧭 Architecture Diagram

