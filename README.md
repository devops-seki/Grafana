# AWS and Azure Monitoring

### This is a solution for creating monitoring for AWS and Azure resources (fast and easy).

---
## AWS

CloudFormation template for adding an EC2 instance with a fully automated bootstrap script to create monitoring that automatically connects to AWS CloudWatch and allows easy viewing of key metrics for AWS resources.
Technologies used: Docker, CloudFormation


<details><summary> Description</summary>
<p>

Run EC2 instance with Docker running containers: Grafana, InfluxDB and Telegraf.

#### This CloudFormation template creates all the resources listed.
 
  - Grafana (EC2)
  - GrafanaSecurityGroup
  - GrafanaIamProfile
  - GrafanaRole
  - GrafanaPolicy

 ![Screen Shot 2022-10-24 at 12 58 36](https://user-images.githubusercontent.com/114985182/197511348-b69d6298-efd6-4e3e-9b18-cc77b135a865.jpg)

---

#### Running CloudFormation template

1. Log in to the AWS account
2. Open CloudFormation and create a stack with new resources
3. Load the template and fill in the parameters
4. Visit EC2 IP address (DNS name) to access the Grafana
   - User: admin
   - Password: admin

</p>
</details>

<details><summary> Video </summary>

https://user-images.githubusercontent.com/114985182/205161844-48b09826-201c-4106-b981-9dbd79ee5975.mp4

</details>

---

## Azure

ARM template for adding an VM with a fully automated bootstrap script to create monitoring that automatically connects to Azure monitor (data source) for metrics and allows users easy viewing of key metrics for Azure resources.

<details><summary> Description</summary>
<p>

### Resources creation for monitoring:
- Resource group
- Virtual network
- Network Interface
- Network security group
- Virtual machine
- Public IP address
- Disk

***Grafana previsioned Data sources***: 
- Azure Monitor for getting metrics on network resources. Credentials will be with User assigned Managed Identity.
- InfluxDB data source in combination with Telegraf for getting metrics on service UpTime.
	
![Screen Shot 2022-11-07 at 21 19 27](https://user-images.githubusercontent.com/114985182/200407339-7eb059a1-53c6-4ba2-9c9a-a38fe8b65380.jpg)


---

#### Running ARM temp from Azure CLI

1. Edit UserData (bootstrap script)

   Open ARM tempate (azuredeploy.json) and Base64 decode userData for VM. After editing variables for the DNS names form script encode it back to Base64. 
   
   ![base64decode](https://user-images.githubusercontent.com/114985182/205156582-99064f93-9a3c-4a91-ba55-62e73ab06a9c.gif)

2. Log in to Azure

   ```Bash
   az login
   ```

3. Set the right subscription

   ```Bash
   az account set --subscription "your subscription id"
   ```

4. Create the Resource group

   ```Bash
   az account list-locations

   az group create --name "resource-group" --location "your location"
   ```

5. Deploy the ARM template

   ```Bash
   az group deployment create --name "name of your deployment" --resource-group "resource-group" --template-file "./azuredeploy.json"
   ```

6. In Azure CLI fill in "Linux OS Password" parameter

-   At least 12 characters
-   A mixture of both uppercase and lowercase letters
-   A mixture of letters and numbers

7. Go to [portal.azure.com](http://portal.azure.com/) and add the role assignment “Monitoring Reader” to the Subscription you want to monitor.

![iam_role_assignment](https://user-images.githubusercontent.com/114985182/200497894-485cf825-7fda-413f-b572-c788b04c5f6d.jpg)
	
8. Visit GrafanaVM IP address (DNS name) to access the Grafana
  
   - User: admin
   - Password: admin

</p>
</details>

<details><summary> Video </summary>

https://user-images.githubusercontent.com/114985182/205161932-5fcb91f8-4ccb-4be1-8571-c2ff3a062dab.mp4

</details>

---


<details><summary>Repository info</summary>
<p>

#### ⚠️  This is a Valcon private repository and it needs a personal access token to be cloned.  ⚠️

The maintainer for the repository: senad.dizdarevic@valcon.com
If you are cloning this repository and creating a new one make sure to change the git clone command in the user-data section of the template.

</p>
</details>