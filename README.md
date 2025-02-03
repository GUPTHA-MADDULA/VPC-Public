<h1> AWS VPC Public Subnet Architecture </h1>

<h2> 📌 Overview </h2>
<p>
This project demonstrates the implementation of an <strong>AWS Virtual Private Cloud (VPC)</strong> with a 
<strong>Public Subnet</strong>. The architecture focuses on securely deploying internet-facing resources such as EC2 instances and Load Balancers in the public subnet while ensuring proper access control, scalability, and high availability.
</p>

<h2> 🔹 VPC Architecture </h2>
![VPC Architecture](https://docs.aws.amazon.com/images/vpc/latest/userguide/images/subnet-diagram.png)

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

