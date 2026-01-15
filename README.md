<img width="500" height="1024" alt="image" src="https://github.com/user-attachments/assets/c9a2ff0d-102e-4b0d-9dd6-0db9eb7bf44a" />

# Secure VM Access with Azure Bastion
Azure Bastion provides `secure RDP and SSH connectivity` to Azure virtual machines without exposing public IPs. This guide walks you through:
- Deploying Azure Bastion
- Configuring Azure Bastion
- Connecting to Windows and Linux VMs via the portal and native clients
- Using sharable links
- Viewing active connections

------
## 🚀 Steps
🔹 Step 1 — Deploy Azure Bastion

<img width="300" height="646" alt="image" src="https://github.com/user-attachments/assets/7cb14f50-f943-4137-b00c-2ee32824ad02" />
<img width="300" height="658" alt="image" src="https://github.com/user-attachments/assets/3fa214f7-e42b-4ea5-b707-32dcd2513fb5" />
<img width="300" height="505" alt="image" src="https://github.com/user-attachments/assets/7e18541c-a807-4af5-9c12-a47526f9274f" />

1. Open the Azure Portal and navigate to your VNet.
2. Check `Subnets`. No Azure Bastion subnet? Add one when creating Bastion.
3. Go to Bastion → Create.
4. Select Manual configuration for full control.
5. Choose Subscription, Resource Group, and Name (e.g., Central Bastion).
6. Set availability zones if supported.
7. Select Standard Tier.
8. Ensure instance count is 2 (default for Standard).
9. Click Next: Virtual Network and select your VNet.
10. Configure a new subnet called `AzureBastionSubnet` (minimum /26).
11. Create or select a Public IP.
12. Click Review + Create and wait for deployment.

----
🔹 Step 2 — Configure Azure Bastion

<img width="300" height="575" alt="image" src="https://github.com/user-attachments/assets/93fb8462-30eb-43c7-a999-ecd1f398c6fc" />
<img width="300" height="508" alt="image" src="https://github.com/user-attachments/assets/61c2db8b-6f9e-478b-8194-be0ba2cd170a" />
<img width="300" height="428" alt="image" src="https://github.com/user-attachments/assets/752b45ad-0fdd-4fcf-8347-d6ebdd23ac79" />

1. Go to the deployed Bastion resource.
2. Access `Overview` and `Settings`.
3. Enable or disable features:
- Copy/Paste
- Private IP connections
- Kerberos authentication (if connected to a domain)
- Native client connections
- Sharable links
4. Premium tier needed for session recording.

-----
🔹 Step 3 — Connect With a Sharable Link

<img width="300" height="431" alt="image" src="https://github.com/user-attachments/assets/f953d9f8-d337-4431-8796-769837454c0c" />

-----
🔹 Step 4 — Connect to a Windows Server from the Azure Portal

<img width="300" height="530" alt="image" src="https://github.com/user-attachments/assets/8946cd99-5a58-48e8-958f-e71f0808c4b3" />
<img width="300" height="591" alt="image" src="https://github.com/user-attachments/assets/8b38b7e7-61df-4e8f-8e31-baaf84428a8b" />

1. Go to the Windows VM → `Connect` → `Bastion`.
2. RDP and port 3389 selected by default.
3. Provide VM username and password.
4. Open in a new browser tab.
5. Connect to access the VM securely.


----
🔹 Step 5 — Connect to a Linux VM via Azure Portal

<img width="300" height="567" alt="image" src="https://github.com/user-attachments/assets/d665aa17-2d59-47bd-b74c-2e568b80e791" />
<img width="300" height="537" alt="image" src="https://github.com/user-attachments/assets/5a73e29e-d01a-4c9e-b078-da603cb8447d" />
<img width="300" height="425" alt="image" src="https://github.com/user-attachments/assets/861487f2-8129-490b-b77d-6e50faa60b6a" />

1. Go to Linux VM → Connect → Bastion.
2. Select SSH.
3. Choose authentication:
- Password
- Azure Key Vault password
- SSH private key (local or Key Vault)
4. Open in a new browser tab and connect.

-----
🔹 Step 6 — Connect to a Windows VM Using Native Client

<img width="400" height="593" alt="image" src="https://github.com/user-attachments/assets/02da9f6c-a752-4581-b564-6343ed68c637" />
<img width="400" height="661" alt="image" src="https://github.com/user-attachments/assets/1ce1c5a9-87c7-44c1-90e3-b0034b433da6" />
<img width="400" height="81" alt="image" src="https://github.com/user-attachments/assets/0f8261c2-7942-469c-94f1-176285ba22ab" />
<img width="400" height="156" alt="image" src="https://github.com/user-attachments/assets/d92b8209-8cb8-48d2-9c58-4af64dc36c28" />
<img width="400" height="492" alt="image" src="https://github.com/user-attachments/assets/ce8c19a7-fc82-4822-a2bb-15a9205a3bb3" />

1. Use Azure CLI to generate connection command for RDP.
2. Log in with `az login`.
3. Paste and run the command.
4. Accept trust prompt and enter VM credentials.
5. Connect via MSTSC/RDP client.

----
🔹 Step 7 — View Active Connections

<img width="500" height="386" alt="image" src="https://github.com/user-attachments/assets/cd08965c-f3ba-45cc-bbce-7a9cf87fadbc" />

1. Go to Bastion → `Settings` → `Sessions`.
2. View current active connections.
3. Close sessions as needed.

----
🔹 Step 8 — Connect to a Linux VM Using Native Client

<img width="500" height="57" alt="image" src="https://github.com/user-attachments/assets/bd95e27d-9b91-4fda-9759-93457bbe6e5d" />
<img width="400" height="486" alt="image" src="https://github.com/user-attachments/assets/94bfa338-b326-4ec9-9ca1-b5cf6ed10975" />

1. Use Azure CLI command for SSH connection.
2. Paste VM resource ID and Bastion details.
3. Authenticate with SSH key.
4. Connect securely to the Linux VM.

## 📦 Example CLI Commands
```
# Log in to Azure CLI
az login

# Connect to a Windows VM via Bastion
az network bastion rdp --name CentralBastion --resource-group RG_NAME --target-resource-id VM_RESOURCE_ID

# Connect to a Linux VM via Bastion
az network bastion ssh --name CentralBastion --resource-group RG_NAME --target-resource-id VM_RESOURCE_ID --auth-type ssh-key --username USER --ssh-key-file PATH
```
