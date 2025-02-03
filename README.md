<h1> AWS VPC Public Subnet Architecture </h1>

<h2> 📌 Overview </h2>
<p>
This project demonstrates the implementation of an <strong>AWS Virtual Private Cloud (VPC)</strong> with a 
<strong>Public Subnet</strong>. The architecture focuses on securely deploying internet-facing resources such as EC2 instances and Load Balancers in the public subnet while ensuring proper access control, scalability, and high availability.
</p>

<h2> 🔹 VPC Architecture </h2>
![VPC Architecture](./images/vpc-example-private-subnets.png)

<h3> 1️⃣ Public Subnet </h3>
<ul>
    <li> The public subnet hosts internet-facing resources such as EC2 instances, Elastic Load Balancers (ELBs), or web servers. </li>
    <li> Connected to an <strong>Internet Gateway (IGW)</strong> that allows internet access for the resources. </li>
    <li> Instances in the public subnet can be accessed from the internet via their public IP addresses. </li>
</ul>

<h3> 2️⃣ Internet Gateway (IGW) </h3>
<ul>
    <li> The Internet Gateway is attached to the VPC to enable internet connectivity for the public subnet. </li>
    <li> It facilitates inbound and outbound traffic for resources in the public subnet. </li>
</ul>

<h3> 3️⃣ Route Tables </h3>
<ul>
    <li> The public subnet uses a route table that directs outbound traffic to the Internet Gateway. </li>
    <li> The route table ensures resources in the public subnet can reach external destinations, such as downloading updates or hosting a website. </li>
</ul>

<h3> 4️⃣ Security Groups & NACLs </h3>
<ul>
    <li> <strong>Security Groups (SGs):</strong> These control the inbound and outbound traffic at the instance level. </li>
    <li> In the public subnet, security groups typically allow HTTP (port 80) and HTTPS (port 443) for web servers and SSH (port 22) for management. </li>
    <li> <strong>Network ACLs (NACLs):</strong> These provide subnet-level security by controlling the inbound and outbound traffic to/from the subnet. </li>
</ul>

<h3> 5️⃣ EC2 Instances in Public Subnet </h3>
<ul>
    <li> EC2 instances are launched in the public subnet, and their security groups ensure that the necessary ports are open to external access. </li>
    <li> These instances are accessible from the internet, which is useful for web servers, APIs, or publicly facing applications. </li>
</ul>

<h2> 🚀 Deployment Steps </h2>

<h3> 1️⃣ Create a VPC </h3>
<pre>
aws ec2 create-vpc --cidr-block 10.0.0.0/16
</pre>

<h3> 2️⃣ Create a Public Subnet </h3>
<pre>
aws ec2 create-subnet --vpc-id vpc-12345678 --cidr-block 10.0.1.0/24 --availability-zone us-east-1a
</pre>

<h3> 3️⃣ Attach Internet Gateway </h3>
<pre>
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --internet-gateway-id igw-12345678 --vpc-id vpc-12345678
</pre>

<h3> 4️⃣ Configure Route Table </h3>
<pre>
aws ec2 create-route-table --vpc-id vpc-12345678
aws ec2 create-route --route-table-id rtb-12345678 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-12345678
aws ec2 associate-route-table --route-table-id rtb-12345678 --subnet-id subnet-12345678
</pre>

<h3> 5️⃣ Launch EC2 Instances in Public Subnet </h3>
<pre>
aws ec2 run-instances --image-id ami-12345678 --count 1 --instance-type t2.micro --subnet-id subnet-12345678 --key-name my-key
</pre>

<h2> 🔒 Security Best Practices </h2>
<ul>
    <li> <strong>Restrict SSH Access:</strong> Allow SSH access only from trusted IP addresses for secure management. </li>
    <li> <strong>Use Security Groups:</strong> Create security groups that only allow necessary ports (HTTP, HTTPS, SSH). </li>
    <li> <strong>Enable VPC Flow Logs:</strong> Monitor and analyze traffic in the VPC for security auditing. </li>
</ul>

<h2> 🛠 Future Enhancements </h2>
<ul>
    <li> Integrate an Elastic Load Balancer (ELB) to distribute traffic among EC2 instances in the public subnet. </li>
    <li> Set up Auto Scaling for better handling of varying web traffic loads. </li>
    <li> Implement CloudWatch for monitoring and alerting on resource health and performance. </li>
</ul>

<h2> 📌 Conclusion </h2>
<p>
This project showcases the implementation of a <strong>public subnet architecture</strong> in AWS, facilitating the deployment of secure, scalable, and internet-facing resources. By following this guide, you can set up a VPC with a public subnet that meets the needs of hosting web applications or APIs.
</p>

