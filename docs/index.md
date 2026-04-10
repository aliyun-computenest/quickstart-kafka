<h1>Kafka Community Edition Service Instance Deployment Documentation</h1>

<h2>Overview</h2>

<p>Kafka is an open-source stream processing platform developed by the Apache Software Foundation, written in Scala and Java. The project aims to provide a unified, high-throughput, and low-latency platform for handling real-time data. Its persistence layer is essentially a "massive publish/subscribe message queue based on a distributed transaction log architecture," making it highly valuable as enterprise-grade infrastructure for processing streaming data.</p>

<h2>Billing Description</h2>

<p>The costs for Kafka Community Edition on Compute Nest mainly involve:</p>

<p><strong>Kafka Cluster:</strong></p>
<ul>
    <li>Selected vCPU and memory specifications</li>
    <li>Disk capacity</li>
    <li>Number of machines</li>
</ul>

<p><strong>ZooKeeper Cluster (if deployed synchronously with Kafka):</strong></p>
<ul>
    <li>Selected vCPU and memory specifications</li>
    <li>Disk capacity</li>
</ul>

<p>Billing methods include:</p>
<ul>
    <li>Pay-As-You-Go (hourly)</li>
    <li>Subscription (Yearly/Monthly)</li>
</ul>

<p>Estimated costs can be viewed in real-time during instance creation.</p>

<h2>Deployment Architecture</h2>

<p>When deploying Kafka Community Edition, you can choose the number of Kafka brokers. According to best practices, the number of brokers must be odd, with a maximum support of 9 nodes. Additionally, during deployment, users can choose whether an existing ZooKeeper cluster is available. If yes, enter the ZooKeeper cluster address; if not, a 3-node ZooKeeper cluster can be launched synchronously.</p>

<h2>Required Permissions for RAM Accounts</h2>

<p>The Kafka service requires access and creation operations for resources such as ECS and VPC. If you use a RAM user to create a service instance, you must add the corresponding resource permissions to the RAM user account before creating the instance. For detailed operations on adding <a href="https://help.aliyun.com/document_detail/121945.html" target="_blank">RAM permissions</a>, please refer to "Authorize RAM Users." The required permissions are listed in the table below.</p>

<table border="1" cellspacing="0" cellpadding="5">
    <thead>
        <tr>
            <th>Permission Policy Name</th>
            <th>Remarks</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>AliyunECSFullAccess</td>
            <td>Permission to manage Elastic Compute Service (ECS)</td>
        </tr>
        <tr>
            <td>AliyunVPCFullAccess</td>
            <td>Permission to manage Virtual Private Cloud (VPC)</td>
        </tr>
        <tr>
            <td>AliyunROSFullAccess</td>
            <td>Permission to manage Resource Orchestration Service (ROS)</td>
        </tr>
        <tr>
            <td>AliyunComputeNestUserFullAccess</td>
            <td>User-side permission to manage Compute Nest services</td>
        </tr>
        <tr>
            <td>AliyunCloudMonitorFullAccess</td>
            <td>Permission to manage Cloud Monitor</td>
        </tr>
    </tbody>
</table>

<h2>Deployment Process</h2>

<h3>Deployment Steps</h3>

<p>Click the <a href="https://computenest.console.aliyun.com/user/cn-hangzhou/serviceInstanceCreate?ServiceId=service-8c341545f86c4f5492e1" target="_blank">deployment link</a> to enter the service instance deployment interface. Follow the prompts on the interface to fill in the parameters and complete the deployment.</p>

<h3>Deployment Parameter Description</h3>

<table border="1" cellspacing="0" cellpadding="5">
    <thead>
        <tr>
            <th>Parameter Group</th>
            <th>Parameter Item</th>
            <th>Example</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="1">Service Instance Name</td>
            <td></td>
            <td>test</td>
            <td>Name of the instance</td>
        </tr>
        <tr>
            <td rowspan="1">Region</td>
            <td></td>
            <td>China (Beijing)</td>
            <td>Select the region for the service instance. It is recommended to select the nearest region to obtain better network latency.</td>
        </tr>
        <tr>
            <td rowspan="1">Billing Configuration</td>
            <td>Billing Method</td>
            <td>Pay-As-You-Go or Subscription</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan="3">Availability Zone & Basic Resource Configuration</td>
            <td>VSwitch Availability Zone</td>
            <td>Zone I</td>
            <td>Different availability zones within the region</td>
        </tr>
        <tr>
            <td>VPC Instance ID</td>
            <td>vpc-xxx</td>
            <td>Select the VPC ID</td>
        </tr>
        <tr>
            <td>VSwitch Instance ID</td>
            <td>vsw-xxxx</td>
            <td>Select the VSwitch ID. If the VSwitch cannot be found, try switching regions and availability zones.</td>
        </tr>
        <tr>
            <td rowspan="5">Kafka ECS Instance Configuration</td>
            <td>Number of Kafka Service Instances</td>
            <td>3</td>
            <td>Number of Kafka brokers. Choose based on business pressure.</td>
        </tr>
        <tr>
            <td>Kafka Service ECS Instance Type</td>
            <td>AMD General Purpose g7a</td>
            <td>Instance specification. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>Kafka System Disk Space</td>
            <td>40</td>
            <td>System disk space. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>Kafka Data Disk Space</td>
            <td>40</td>
            <td>Data disk space. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>Kafka Instance Password</td>
            <td>****</td>
            <td>Set the instance password. Length: 8-30 characters. Must contain at least three of the following: uppercase letters, lowercase letters, digits, and special symbols ()`!@#$%^&*-+={}[]:;'<>,.?/</td>
        </tr>
        <tr>
            <td rowspan="6">ZooKeeper Cluster Configuration</td>
            <td>Existing ZooKeeper Cluster?</td>
            <td>true</td>
            <td>Select based on actual situation.</td>
        </tr>
        <tr>
            <td>ZooKeeper Address (if cluster exists)</td>
            <td>10.x.x.0:2181</td>
            <td>Separate multiple addresses with half-width commas, e.g., 10.x.x.0:2181,10.x.x.1:2181</td>
        </tr>
        <tr>
            <td>ZooKeeper Service ECS Instance Type (if no cluster)</td>
            <td>AMD General Purpose g7a</td>
            <td>Instance specification. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>ZooKeeper System Disk Space (if no cluster)</td>
            <td>40</td>
            <td>System disk space. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>ZooKeeper Data Disk Space (if no cluster)</td>
            <td>40</td>
            <td>Data disk space. Choose based on actual requirements.</td>
        </tr>
        <tr>
            <td>ZooKeeper Instance Password (if no cluster)</td>
            <td>****</td>
            <td>Set the instance password. Length: 8-30 characters. Must contain at least three of the following: uppercase letters, lowercase letters, digits, and special symbols ()`!@#$%^&*-+={}[]:;'<>,.?/</td>
        </tr>
    </tbody>
</table>

<h3>Verification Results</h3>

<ol>
    <li>
        <p><strong>View Service Instance:</strong> After the service instance is successfully created, the deployment takes approximately 2 minutes. Once deployment is complete, the corresponding service instance will be visible on the page.</p>
    </li>
    <li>
        <p><strong>Access Kafka via Service Instance:</strong></p>
    </li>
</ol>

<h3>Using Kafka</h3>

<p>Please visit the official Kafka website for full usage information: <a href="https://kafka.apachecn.org/" target="_blank">Kafka Trial Documentation</a></p>
