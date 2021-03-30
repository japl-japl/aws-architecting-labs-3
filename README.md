# aws-architecting-labs-3
Automation of Creating a VPC on AWS


Automation of Creating a VPC on AWS

<div class="Box-body px-5 pb-5">


<article class="markdown-body entry-content container-lg" itemprop="text"><h1><a id="user-content-lab-2-creating-a-vpc-and-deploying-a-web-app" class="anchor" aria-hidden="true" href="#lab-2-creating-a-vpc-and-deploying-a-web-app"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Lab 3 - Creating a Virtual Private Cloud (VPC)</h1>

<p>Tradional networking is difficult - it envolves equipment, cabling, complex configurations, and special skills. Fortunately, Amazon Virtual Private Cloud (Amazon VPC) hides the complexity while making it easy to deploy secure private networks.</p>

<p>This Lab shows you how to build your own VPC, create subnets, and direct traffic between VPC components.</p>

<p>An optional challenge is available. In the challenge task, your create a VPC peering connection to a shared services VPC. Then you use an application and database to test connectivity between the VPCs.</p>

<h2><a id="user-content-task-1-create-a-vpc" class="anchor" aria-hidden="true" href="#task-1-create-a-vpc"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 1: Create a VPC</h2>

<p>You'll begin by creating a VPC. You could use the wizard to make it as simple as possible but here we'll do it with CloudFormtion.</p>

<ol>

<li>

<p>In <strong>Services-&gt;VPC</strong> click <strong>Your VPCs</strong> on the left, and then click on <strong>Create VPC</strong>.</p>

</li>

<li>

<p>For <strong>Name tag</strong> give it the name firstname-lastname-vpc (replace firstname with your firstname in lowercase and lastname with your lastname in lowercase). For <strong>IPv4 CIDR block</strong> put 10.0.0.0/16. Then click <strong>Create</strong> and <strong>Close</strong></p>

</li>

<li>

<p>Click the checkbox next to the VPC you just created in the last (make sure it is the only one selected and deselect any other if they are also selected). Click on the <strong>Actions</strong> button and click <strong>Edit DNS hostnames</strong>. Click the checkbox next to <strong>enable</strong> and click

<strong>Save</strong> and then <strong>Close</strong></p>

</li>

</ol>

<p>This will assign friendly dns names to your instances when they are added to the vpc. The names will have a format that looks like ec2-52-42-133-255.us-west-2.compute.amazonaws.com where us-west-2 is the region that your VPC is in and the first portion matches the public IP address of your instance. You could change this to a more meaningful name by using Route 53 (the AWS DNS service)</p>

<h2><a id="user-content-task-2-create-subnets" class="anchor" aria-hidden="true" href="#task-2-create-subnets"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 2: Create subnets</h2>

<p>Now you'll add some subnets to the VPC. One public and one private subnet.</p>

<ol>

<li>In the left-hand pane click <strong>Subnets</strong>, then click <strong>Create subnet</strong>. Give it the <strong>Name tag</strong> firstname-lastname-public and select your VPC in the <strong>VPC</strong> dropdown selector. Select the first <strong>Availability Zone</strong> in the dropdown selector list and set the <strong>IPv4 CIDR block</strong> to 10.0.0.0/24. Then click <strong>Create</strong> and <strong>Close</strong></li>

</ol>

<p>Note: you have to select a CIDR range for the subnet that is inside the CIDR range of the VPC it is in. and 10.0.0.0/24 is within 10.0.0.0/16.</p>

<ol start="2">

<li>Select the subnet you just created via the checkbox to the left of it in the list and click <strong>Actions</strong> and <strong>Modify auto-assign IP settings</strong>. Click the checkbox next to <strong>Auto-assign IPv4</strong> and click <strong>Save</strong>.</li>

</ol>

<p>This will automatically assign a public IPv4 address to all EC2 instances as they are added to the subnet. However this subnet is not truly public yet until we add an Internet Gateway to connect it to the internet (which you'll do in the next task).</p>

<ol start="3">

<li>Repeat the steps once more to create one private subnet named firstname-lastname-private with IP range 10.0.2.0/23.</li>

</ol>

<p>Note this range is also within the VPC range and it is twice as large as the public range. This is typical as most of your resources shoudl be in private subnets and so they need larger IP spaces to be able to assign IP addresses to larger numbers of resources.</p>

<h2><a id="user-content-task-3-create-an-internet-gateway" class="anchor" aria-hidden="true" href="#task-3-create-an-internet-gateway"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 3: Create an internet gateway</h2>

<p>Now you will add an internet gateway to add internet connectivity to VPC and then you'll set up that internet gateway to provide the connectivity to the public subnet your created. An internet gateway is a horizontally scaled redundant high capacity service. It

does not place any availability risk (due to failure) or bandwith limits on traffic between the internet and your VPC.</p>

<p>The internet gateway provides a target for your route tables to connect to the internet and also provides the NAT (network address translation) for instances with public IP addresses.</p>

<ol>

<li>

<p>In the left-hand pane click <strong>Internet gateways</strong> then click <strong>Create internet gateway</strong>. Give it the name firstname-lastname-igw then click <strong>Create</strong> and <strong>Close</strong></p>

</li>

<li>

<p>Select the newly create internet gatway (make sure its the only one selected) and click <strong>Action</strong> then <strong>Attach to VPC</strong>. Select your VPC and click <strong>Attach</strong></p>

</li>

</ol>

<p>Your VPC is now connected to the internet but you will need to update the route table for your public subnet to use it to connect to the internet.</p>

<h2><a id="user-content-task-4-configure-route-tables" class="anchor" aria-hidden="true" href="#task-4-configure-route-tables"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 4: Configure route tables</h2>

<p>A route table includes a set of routes which are rules for where to send traffic which destination IP addresses that match the routes. Each subnet must be connected to a subnet which controls where traffic from that subnet can be routed. A subnet can only be associated with one route table at a time, but multiple subnets can be associated with the same route table.</p>

<p>For a subnet to use the internet gateway it needs to have a route in its route table that points internet-bound traffic at the internet gateway. Subnets that have such routes are known as <em>Public subnets</em></p>

<ol>

<li>

<p>In the left-hand pane click <strong>Route Tables</strong>. In the list look for the one that is currently in use for your vpc. You can tell by looking at the <strong>Summary</strong> tab below and you'll see the <strong>VPC</strong> field will have the name of your VPC in it. If you click on the <strong>Routes</strong> tab you will see it has a single route and the <strong>Target</strong> is local (so this is a private route table that does not connect to the internet).</p>

</li>

<li>

<p>Click on the pencil icon in the <strong>Name</strong> column for this route table and give it the <strong>Name</strong> firstname-lastname-private-rt</p>

</li>

<li>

<p>Click <strong>Create route table</strong> and set <strong>Name tag</strong> to firstname-lastname-public-rt and <strong>VPC</strong> to your create VPC. Click <strong>Create</strong> and <strong>Close</strong></p>

</li>

<li>

<p>Select the newly created route table in the list via the checkbox to the left (make sure it is the only one selected). Click on the <strong>Routes</strong> tab, and click the <strong>Edit routes</strong> button and <strong>Add route</strong> button. Put 0.0.0.0/0 in <strong>Destination</strong> and the select <strong>Internet gateway</strong> in the <strong>Target</strong> selector and then click on your internet gateway, and then click <strong>Save routes</strong> and <strong>Close</strong></p>

</li>

</ol>

<p>Now we have to associate this new public route table with the public subnet</p>

<ol start="5">

<li>Click the <strong>Subnet associations</strong> tab and click the <strong>Edit subnet associations</strong> button, select your public subnet via the checkbox to the left of it, and click <strong>Save</strong></li>

</ol>

<p>Now your public subnet is truly public as it can send and receive traffic into the internet. To summarize, to make a subnet public requires creating (or already having) an internet gateway in your VPC, creating a route table (or adding a route to an existing route table) that points 0.0.0.0/0 destinatation traffic to that internet gateway, and associating that route table with the subnet which you want to be public (which then becomes public)</p>

<h2><a id="user-content-task-5-create-security-groups" class="anchor" aria-hidden="true" href="#task-5-create-security-groups"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 5: Create Security groups</h2>

<p>In this task you will create Security groups to lock down the type of traffic that can flow into your App server and Database (to be added later)</p>

<ol>

<li>

<p>In <strong>Services-&gt;EC2</strong> click on <strong>Security Groups</strong> in the left-hand navigation panel</p>

</li>

<li>

<p>Click the <strong>Create Security Group</strong> button and then set the <strong>Security group name</strong> to <strong>firstname-lastname-app-sg</strong>, <strong>Description</strong> to <strong>Allow HTTP traffic</strong>, and <strong>VPC</strong> to your created VPC (firstname-lastname-vpc), then click <strong>Create</strong>. This security group will be used to allow HTTP traffic into your app server</p>

</li>

<li>

<p>Select the security group you just created (via checkbox to the left of it in the list), and click the <strong>Actions-&gt;Edit inbound rules</strong> option and then click the <strong>Add Rule</strong> button, set <strong>Type</strong> to <strong>HTTP</strong> and <strong>Source</strong> to <strong>Anywhere</strong> and click <strong>Save rules</strong></p>

</li>

<li>

<p>Select the security group you just created and copy the <strong>Group ID</strong> displayed in the <strong>Description</strong> tab in the lower half of the page</p>

</li>

<li>

<p>Click the <strong>Create Security Group</strong> button and then set the <strong>Security group name</strong> to <strong>firstname-lastname-db-sg</strong>, <strong>Description</strong> to <strong>Allow DB access</strong>, and <strong>VPC</strong> to your created VPC (firstname-lastname-vpc), then click <strong>Create</strong>. This security group will be used to allow DB traffic to come from your app server to your database</p>

</li>

<li>

<p>Select the security group you just created (via checkbox to the left of it in the list), and click the <strong>Actions-&gt;Edit inbound rules</strong> option and then click the <strong>Add Rule</strong> button, set <strong>Type</strong> to <strong>MYSQL/Aurora</strong> and <strong>Source</strong> to the <strong>Group ID</strong> you copied in step 4, then click <strong>Create</strong></p>

</li>

</ol>

<h2><a id="user-content-task-7-create-an-app-server" class="anchor" aria-hidden="true" href="#task-7-create-an-app-server"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Task 6: Create an App Server</h2>

<p>In this task you will create a IAM role and then use that IAM role as the Instance profile when creating an EC2 instance that will be the App Server</p>

<ol>

<li>

<p>In <strong>Services-&gt;IAM</strong>, in the left-hand menu select <strong>Policies</strong>, then click <strong>Create policy</strong></p>

</li>

<ol start="3">

<li>

<p>For the <strong>Name</strong> use <strong>firstname-lastname-inventory-policy</strong>, then click <strong>Create policy</strong></p>

</li>

<li>

<p>Next, click on <strong>Roles</strong> in the left-hand menu, then click <strong>Create role</strong></p>

</li>

<li>

<p>Leave the <strong>Select type of trusted entity</strong> to <strong>AWS Service</strong> and click on <strong>EC2</strong> in the <strong>Choose the service that will use this role</strong> section, then click <strong>Next:Permissions</strong></p>

</li>

<li>

<p>In the search bar enter the policy you had created earlier (firstname-lastname-policy), it should appear in the list below, select the checkbox to the left of it and click <strong>Next:Tags</strong> and then click <strong>Next:Review</strong></p>

</li>

<li>

<p>For <strong>Role name</strong> put firstname-lastname-inventory-role and click <strong>Create role</strong></p>

</li>

<li>

<p>In <strong>Services-&gt;EC2</strong>, click <strong>Launch instance</strong>, and click <strong>Select</strong> to the right of the AMI at the top of the list (Amazon Linux 2 AMI (HVM), SSD Volume Type)</p>

</li>

<li>

<p>Leave instance as-is (t2.micro) and click <strong>Next:Configure Instance Details</strong>, set <strong>Network</strong> to your created vpc (firstname-lastname-vpc) and set the <strong>Subnet</strong> to your public subnet (firstname-lastname-public), set <strong>Auto-assign Public IP</strong> to <strong>Enable</strong>, set <strong>IAM role</strong> to the role you created above (firstname-lastname-inventory-role)</p>

</li>

<li>

<p>Scroll down and click on the <strong>Advanced Details</strong> section to open it, then paste the following script text into the <strong>User data</strong> editor pane</p>

</li>

</ol>

<div class="highlight highlight-source-shell"><pre><span class="pl-c"><span class="pl-c">#!</span>/bin/bash</span>

<span class="pl-c"><span class="pl-c">#</span> Install Apache Web Server and PHP</span>

yum install -y httpd mysql

amazon-linux-extras install -y php7.2

<span class="pl-c"><span class="pl-c">#</span> Download Lab files</span>

wget https://us-west-2-tcprod.s3.amazonaws.com/courses/ILT-TF-100-ARCHIT/v6.5.0/lab-2-webapp/scripts/inventory-app.zip

unzip inventory-app.zip -d /var/www/html/

<span class="pl-c"><span class="pl-c">#</span> Download and install the AWS SDK for PHP</span>

wget https://github.com/aws/aws-sdk-php/releases/download/3.62.3/aws.zip

unzip aws -d /var/www/html

<span class="pl-c"><span class="pl-c">#</span> Turn on web server</span>

chkconfig httpd on

service httpd start</pre></div>

<p>This script will run at instance start-up, it will install a mysql client, php, and an apache web-server, it will then download and install some php code for an application and the AWS SDK for php and will start the apache web server</p>

<ol start="11">

<li>

<p>Click <strong>Next:Add Storage</strong> and then click <strong>Next:Add Tags</strong>, click <strong>Add Tag</strong> and set <strong>Key</strong> to <strong>Name</strong> and <strong>Value</strong> to firstname-lastname-app-server, then click <strong>Next:Configure Security Group</strong></p>

</li>

<li>

<p>Click <strong>Select an existing security group</strong> and click the checkbox to the left of your app server security group (firstname-lastname-app-sg), then click <strong>Review and launch</strong>, click <strong>Continue</strong> in the warning dialog, then click <strong>Launch</strong></p>

</li>

<li>

<p>In the dialog in the top dropdown, select <strong>Proceed without a keypair</strong>, click on the acknolwedgement checkbox, and click <strong>Launch Instances</strong>, then click <strong>View Instances</strong></p>

</li>

</ol>

<h2><a id="user-content-task-8-test-the-application" class="anchor" aria-hidden="true" href="#task-8-test-the-application"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>CHALLENGE: CONFIGURE VPC PERRTING</h2>

<p>In this task you will verify that the web application is working correctly</p>

<ol>

<li>

<p>In the Instances page click on the checkbox to the left of your app server instance (firstname-lastname-app-server), scroll down to the bottom panel and copy the <strong>IPv4 Public IP</strong> and open a new browser tab with URL set to that IP address</p>

</li>

<li>

<p>You should see a web-app open in the browser tab and you should see a <strong>Settings</strong> button, click on it</p>

</li>

<li>

<p>In the form, put <strong>inventory</strong> for the <strong>Database</strong>, <strong>master</strong> for the <strong>Username</strong>, and <strong>lab-password</strong> for the <strong>Password</strong></p>

</li>

<li>

<p>In the browser tab with your AWS management console, click on <strong>Services-&gt;RDS</strong> and then <strong>Databases</strong> in the left-hand menu</p>

</li>

<li>

<p>Click on the the database you had created (firstname-lastname-inventory-db), you should click on the name itself, not the radio button to the left.</p>

</li>

<li>

<p>Look for the <strong>Endpoint</strong> in the <strong>Connectivity &amp; security</strong> section and copy it</p>

</li>

<li>

<p>Return to the browser tab open to your web application and paste the endpoint into the <strong>Endpoint</strong> field and click <strong>Save</strong>.</p>

</li>

</ol>

<p>You should now see a list of pre-created data, you can go ahead and delete that and create new entries (these will be created in the database from the app server web application).</p>

</article>

</div>

</div>



</div>







</div>

</div>



</main>

</div>



</div>

<h1><span style="color: #ff0000;"><strong>I hope this would be helpful to you.</strong></span></h1>
