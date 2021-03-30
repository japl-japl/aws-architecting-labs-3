# aws-architecting-labs-3
Automation of Creating a VPC on AWS


<!DOCTYPE html>
<html lang='en'>
<head>
<meta content='[]' name='active-experiments'>
<meta content='{&quot;userId&quot;:332}' name='help-api-product-data'>
<meta name="csrf-param" content="authenticity_token" />
<meta name="csrf-token" content="5X4wyRma2cutFaWvqkatkXzwV4SDXPHnYvXdMnXO6OMO3YYDKG2KGwFYEp/J4IQzO3trAC4s7GV0Aaq8bm862Q==" />
<title>Architecting on AWS - Lab 4 - Creating a Highly Available Environment | Qwiklabs</title>
<meta content='width=device-width, initial-scale=1.0, maximum-scale=1, user-scalable=0' name='viewport'>
<meta content='1rRsY0INj8RvwB5EF5pwdxt2A2P9aDgAlsICaJ0d5w0' name='google-site-verification'>
<meta content='#3681E4' property='msapplication-TileColor'>
<meta content='/favicon-144.png' property='msapplication-TileImage'>
<meta content='In this lab, you will start with an application running on a single Amazon EC2 instance and will then convert it to be Highly Available.' name='description'>
<meta content='Qwiklabs' name='author'>
<meta content='Architecting on AWS - Lab 4 - Creating a Highly Available Environment | Qwiklabs' property='og:title'>
<meta content='website' property='og:type'>
<meta content='/favicon-144.png' property='og:image'>
<meta content='Qwiklabs' property='og:site_name'>
<meta content='In this lab, you will start with an application running on a single Amazon EC2 instance and will then convert it to be Highly Available.' property='og:description'>
<meta content='/qwiklabs_logo_900x887.png' property='og:logo' size='900x887'>
<meta content='/qwiklabs_logo_994x187.png' property='og:logo' size='994x187'>
<link href='/favicon-32.png' rel='shortcut icon'>
<link color='#3681E4' href='/favicon-svg.svg' rel='mask-icon'>
<link href='/favicon-180.png' rel='apple-touch-icon-precomposed'>
<link rel="stylesheet" media="screen" href="https://fonts.googleapis.com/css?family=Oswald:400|Roboto+Mono:400,700|Roboto:300,400,500,700|Google+Sans:300,400,500,700|Google+Sans+Display:400|Material+Icons|Google+Material+Icons" />


<!--[if lt IE 9]>
<script src='http://html5shim.googlecode.com/svn/trunk/html5.js' type='text/javascript'></script>
<![endif]-->
<!--[endif]>  <![endif]-->
<script>
//<![CDATA[
window.gon={};gon.current_user={"firstname":"Victor","lastname":"Dur\u00e1n","fullname":"Victor Dur\u00e1n","company":"HiQ Stockholm","email":"victor.duran@hiq.se","origin":"informator, direct","subscriptions":0,"id":"17137556c40920f3be9c66b968f8da44","qlCreatedAt":"2020-12-07 09:18:47 UTC","optIn":true};gon.segment=null;gon.deployment="informator";
//]]>
</script>
<script type='application/ld+json'>
{
  "@context": "http://schema.org",
  "@type": "WebSite",
  "url": "https://www.qwiklabs.com/",
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://www.qwiklabs.com/catalog?keywords={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}
</script>
<script id='ze-snippet' src='https://static.zdassets.com/ekr/snippet.js?key=511e4158-0aec-4e3c-b2e6-4daa1769f51e'></script>



<link rel="stylesheet" media="all" href="https://cdn.qwiklabs.com/assets/application-9332cbbc707f820b62968bb61954dfc42bef3914e2cc31109a2e41ac9b745e29.css" />
<script>
  EVENT_SOURCE_BASE_URL = "https://informator.qwiklabs.com/nchan-sub?id=";
</script>
<script src="https://cdn.qwiklabs.com/assets/hallofmirrors/polyfills/webcomponents-loader-408088dc333247a761de5f2b2a4ba1cabd2bc36579f83ba92a559eb3682a9b77.js"></script>
<script src="https://cdn.qwiklabs.com/assets/hallofmirrors/hallofmirrors-4f8a6cfa9711d032a110cd56effd69430c4851f482ed96db0c2ecf05bb26be22.js"></script>
<script src="https://www.youtube.com/iframe_api"></script>
<script src="https://cdn.qwiklabs.com/assets/vendor-45d462772c30000424907184f70c7157e95fb6227698d1671c5051818a6f60d8.js"></script>
<script src="https://cdn.qwiklabs.com/assets/application-6915c7e0b283bc022c42b5fae6aec665576ef117127c2938d292c7ce886b5992.js"></script>
</head>
<body class='application-new focuses focuses-show l-full lab-show no-nav'>
<div class='header-container'>
<div class='header'>
<ql-icon-button class='js-nav-toggle header__nav-panel-button l-mrm'>menu</ql-icon-button>
<div class='header__title'>
<a class="icon-button" href="/classrooms/51"><ql-icon>arrow_back</ql-icon></a>

<h1 class='headline-5'>
Architecting on AWS - Lab 4 - Creating a Highly Available Environment
</h1>
</div>
<div class='header__actions'>
<ql-icon-button class='header__button--search js-header-search-bar-button'>search</ql-icon-button>
<ql-icon-button id='control-panel-target' style='display: none;'>
dashboard
</ql-icon-button>
<ql-menu for='#control-panel-target' id='control-panel-menu'></ql-menu>

<ql-icon-button id='help-menu-button'>help</ql-icon-button>
<ql-menu for='#help-menu-button' id='help-menu'>
<ql-menu-item>
<ql-help context='lab' data-analytics-action='opened_help' data-analytics-label='lab' productdata='{&quot;userId&quot;:332}'>
Help Center
</ql-help>
</ql-menu-item>
<ql-menu-item>
<a target="_blank" class="ql-body-1" href="https://support.google.com/qwiklabs/contact/contact_us">Email support</a>
</ql-menu-item>
<ql-menu-item>
<a class='ql-body-1' onClick='ql.chat.open()'>Chat support</a>
</ql-menu-item>
</ql-menu>

<button class='icon-button' id='my_account'>
<img class="avatar " alt="avatar image" src="https://secure.gravatar.com/avatar/596d7f9d482af692e44dc70621fa0763.png?s=80&amp;d=mm" />
</button>
<ql-menu for='#my_account' open>
<div class='my-account-menu'>
<img class="avatar " alt="avatar image" src="https://secure.gravatar.com/avatar/596d7f9d482af692e44dc70621fa0763.png?s=80&amp;d=mm" />
<div class='my-account-menu__user-info l-mbl'>
<h4 class='ql-subhead-1'>Victor Durán</h4>
<p class='ql-body-2 text--light'>victor.duran@hiq.se</p>
<p class='ql-body-2 text--light'>
</p>
</div>
<div class='buttons l-mbl'>
<a class="button button--hairline" id="settings" href="/my_account/profile">Settings</a>
</div>
<hr>
<ql-button data-analytics-action='clicked_sign_out' href='/users/sign_out' method='delete'>
Sign Out
</ql-button>
<div class='privacy l-mtl'>
<a class="ql-caption text--light" href="/privacy_policy">Privacy</a>
<span class='ql-caption text--light l-mls l-mrs'>&middot;</span>
<a class="ql-caption text--light" href="/terms_of_service">Terms</a>
</div>
</div>
</ql-menu>

</div>
</div>
<div class='header__search-bar js-header-search-bar'>
<form class="js-search-form-mobile" onsubmit="ql.searchFilter(); return false;" action="/searches/lab" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><input type="hidden" name="authenticity_token" value="8FT/1lwmLbNv5uGQzl7+tpOHfx8/P4A8w2zMXzY9Pbwb90kcbdF+Y8OrVqCt+NcU1AxDm5JPnb7VmLvRLZzvhg==" />
<input type="text" name="keywords" id="keywords" placeholder="Search" maxlength="255" aria-label="catalog search bar" />
</form>

<ql-icon-button class='js-close-search-bar'>close</ql-icon-button>
</div>
</div>

<nav class='nav-bar'>
<a class="nav-bar__item js-navigation-button" href="/"><ql-icon class='nav-bar__item__icon'>
home
</ql-icon>
<span class='nav-bar__item__label'>
Home
</span>
</a>
<a class="nav-bar__item js-navigation-button" href="/catalog"><ql-icon class='nav-bar__item__icon'>
school
</ql-icon>
<span class='nav-bar__item__label'>
Catalog
</span>
</a>
<a class="nav-bar__item js-navigation-button  active" aria-current="page" href="/my_learning"><ql-icon class='nav-bar__item__icon'>
event_note
</ql-icon>
<span class='nav-bar__item__label'>
My Learning
</span>
</a>
</nav>

<nav class='nav-panel js-nav-panel'>
<div class='nav-panel__logo'>
<div class='custom-logo'><img src="https://s3.amazonaws.com/qwiklab-config/Informator+logo.png" /></div>
</div>
<a title="Home" tabindex="-1" class="nav-panel__item js-navigation-button" href="/"><ql-icon class='nav-panel__item__icon'>
home
</ql-icon>
<div class='nav-panel__item__label'>
Home
</div>
</a>
<a title="Catalog" tabindex="-1" class="nav-panel__item js-navigation-button" href="/catalog"><ql-icon class='nav-panel__item__icon'>
school
</ql-icon>
<div class='nav-panel__item__label'>
Catalog
</div>
</a>
<a title="My Learning" tabindex="-1" class="nav-panel__item js-navigation-button active" aria-current="page" href="/my_learning"><ql-icon class='nav-panel__item__icon'>
event_note
</ql-icon>
<div class='nav-panel__item__label'>
My Learning
</div>
</a>
<div class='nav-panel__spacer'></div>
<a title="Profile" tabindex="-1" class="nav-panel__item js-navigation-button" href="/my_account/profile"><ql-icon class='nav-panel__item__icon'>
account_circle
</ql-icon>
<div class='nav-panel__item__label'>
Profile
</div>
</a>
<a title="Credits &amp; Subscriptions" tabindex="-1" class="nav-panel__item js-navigation-button" href="/my_account/credits"><ql-icon class='nav-panel__item__icon'>
money
</ql-icon>
<div class='nav-panel__item__label'>
Credits &amp; Subscriptions
</div>
</a>
<a title="Security" tabindex="-1" class="nav-panel__item js-navigation-button" href="/my_account/security"><ql-icon class='nav-panel__item__icon'>
security
</ql-icon>
<div class='nav-panel__item__label'>
Security
</div>
</a>
<div class='nav-panel__spacer'></div>
<a class="nav-panel__item" tabindex="-1" href="#"><ql-help>
<div class='nav-panel__help-item'>
<ql-icon class='nav-panel__item__icon'>help</ql-icon>
<div class='nav-panel__item__label'>Help</div>
</div>
</ql-help>
</a><div class='nav-panel__small-links'>
<a tabindex="-1" href="/privacy_policy">Privacy</a>
<a tabindex="-1" href="/terms_of_service">Terms</a>
</div>
</nav>
<div class='nav-panel__overlay js-nav-toggle'></div>

<div class='cookie-bar'>
<span>
This site uses cookies from Google to deliver its services and to analyze traffic.
</span>
<div class='buttons'>
<a class='button button--outline' href='https://policies.google.com/technologies/cookies' target='_blank'>
Learn More.
</a>
<a class='button button--positive js-accept-cookies'>
Ok, Got it.
</a>
</div>
</div>

<main class='js-main'>
<span class='hidden' id='flash-sibling-before'></span>

<div class='l-main-wrapper' id='main-wrapper'>







<ql-drawer-container class='js-lab-state' data-analytics-payload='{&quot;label&quot;:&quot;Architecting on AWS - Lab 4 - Creating a Highly Available Environment&quot;,&quot;lab_name&quot;:&quot;Architecting on AWS - Lab 4 - Creating a Highly Available Environment&quot;,&quot;classroom_name&quot;:null,&quot;deployment&quot;:&quot;informator&quot;}' data-focus-id='352' data-lab-billing-limit='0.0' data-lab-duration='10800' data-parent='classroom' id='lab-container'>
<ql-drawer id='terminal-drawer' slot='drawer'>
<ql-cloud-terminal class='terminal'></ql-cloud-terminal>
</ql-drawer>
<ql-drawer-content class='js-lab-wrapper' id='lab-content' slot='drawer-content'>
<ql-drawer-container id='lab-content-container'>
<ql-drawer id='control-panel-drawer' open slot='drawer' width='320'>
<ql-lab-control-panel class='ql-lab-control-panel__max-height control-panel js-lab-control-panel' connectionFiles='[]' labControlButton='{&quot;disabled&quot;:false,&quot;pending&quot;:false,&quot;running&quot;:false}' labDetails='[]' labTimer='{&quot;ticking&quot;:false,&quot;secondsRemaining&quot;:10800}' studentResources='[]'>
</ql-lab-control-panel>
</ql-drawer>
<ql-drawer-content id='lab-instructions' slot='drawer-content'>
<div class='alert alert--fake js-alert'>
<p class='alert__message js-alert-message'></p>
<a class='alert__close js-alert-close'>
<i class='fa fa-times'></i>
</a>
<iframe class='l-ie-iframe-fix'></iframe>
</div>
<div class='js-lab-content lab-content__renderable-instructions'>
<div class='lab-preamble'>
<h1 class='lab-preamble__title'>
Architecting on AWS - Lab 4 - Creating a Highly Available Environment
</h1>
<div class='lab-preamble__details subtitle-headline-1'>
<span>3 hours </span>
<span>Free</span>
<div class='lab__rating'>
<a href="/focuses/352/reviews?parent=catalog"><div class='rateit' data-rateit-readonly='true' data-rateit-value='0'></div>

</a><a data-target='#lab-review-modal' data-toggle='modal'>
Rate Lab
</a>
</div>
</div>
</div>

<div class='js-markdown-instructions markdown-lab-instructions no-select' id='markdown-lab-instructions'>
<p><img src="https://s3-us-west-2.amazonaws.com/us-west-2-aws-training/awsu-spl/sts-sign-in-images/media/aws-logo.png" alt=""></p>



<p>© 2020 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited. All trademarks are the property of their owners.</p>

<p>Corrections, feedback, or other questions? Contact us at <a href="https://support.aws.amazon.com/#/contacts/aws-training" target="_blank"><em>AWS Training and Certification</em></a>.</p>

Lab overview

<p>Critical business systems should be deployed as highly available applications, meaning that they can remain operational even when some components fail. To achieve high availability in AWS, it is recommended to run services across multiple Availability Zones.</p>

<p>Many AWS services are inherently highly available, such as load balancers. You can configure other services for high availability, such as deploying Amazon Elastic Compute Cloud (Amazon EC2) instances in multiple Availability Zones.</p>

<p>In this lab, you start with an application running on a single Amazon EC2 instance and then convert it to be highly available. You create an Application Load Balancer and Auto Scaling group, update the security groups, and test to ensure the application is highly available.</p>

<p>The following image shows the final architecture:</p>

<p><img src="https://us-east-1-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-4-ha/instructions/en_us/images/architecture.png" alt="Architecture"></p>

<p>Two optional <strong>Challenge</strong> tasks are available. The first is to make the database highly available. The second is to make the NAT Gateway highly available.</p>

<p><strong>Objectives</strong></p>

<p>After completing this lab, you will be able to:</p>
<ul>
<li>Create an Application Load Balancer</li>
<li>Create an Amazon EC2 Auto Scaling group</li>
<li>Update security groups to enforce a three-tier architecture</li>
</ul>
<p><strong>Duration</strong></p>

<p>The lab requires approximately <strong>40 minutes</strong> to complete.</p>



<h2 id="step2">Start Lab</h2>
<ol start="1">
<li>At the top of your screen, launch your lab by choosing <span style="background-color:#34A853;font-family:Google Sans;font-weight:bold;font-size:90%;color:white;border-color:#34A853;border-radius:4px;border-width:2px;border-style:solid;padding-top:5px;padding-bottom:5px;padding-left:10px;padding-right:10px;">Start Lab</span>
</li>
</ol>
<p>This starts the process of provisioning your lab resources. An estimated amount of time to provision your lab resources is displayed. You must wait for your resources to be provisioned before continuing.</p>

<p><i class="fas fa-info-circle"></i> If you are prompted for a token, use the one distributed to you (or credits you have purchased). </p>
<ol start="2">
<li>Open your lab by choosing <span style="background-color:white;font-family:Google Sans;font-weight:bold;font-size:90%;color:#1a73e8;border-color:#dadce0;border-radius:4px;border-width:2px;border-style:solid;padding-top:5px;padding-bottom:5px;padding-left:10px;padding-right:10px;">Open Console</span>
</li>
</ol>
<p>This opens an AWS Management Console sign-in page.</p>
<ol start="3">
<li>On the sign-in page, configure:</li>
</ol><ul>
<li>
<strong>IAM user name:</strong> <input readonly class="copyable-inline-input" size="10" type="text" value="awsstudent">
</li>
<li>
<strong>Password:</strong> Paste the value of <strong>Password</strong> from the left side of the lab page</li>
<li>Choose <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Sign In</span>
</li>
</ul>
<p><i class="fas fa-exclamation-triangle"></i> <strong>Do not change the Region unless instructed.</strong></p>



<h3>Common Login Errors</h3>

<p><strong>Error: You must first log out</strong></p>

<p><img src="https://s3-us-west-2.amazonaws.com/us-west-2-aws-training/awsu-spl/sts-sign-in-images/media/logouterror.png" alt=""></p>

<p>If you see the message, <strong>You must first log out before logging into a different AWS account:</strong> </p>
<ul>
<li>Choose <strong>click here</strong>
</li>
<li>Close your browser tab to return to your initial lab window</li>
<li>Choose <span style="background-color:white;font-family:Google Sans;font-weight:bold;font-size:90%;color:#1a73e8;border-color:#dadce0;border-radius:4px;border-width:2px;border-style:solid;padding-top:5px;padding-bottom:5px;padding-left:10px;padding-right:10px;">Open Console</span> again</li>
</ul>


<h2 id="step3">Task 1: Inspecting your VPC</h2>

<p>As part of the lab, the following resources have already been provisioned for you via AWS CloudFormation:</p>
<ul>
<li>An Amazon Virtual Private Cloud (Amazon VPC)</li>
<li>Public and private subnets in two Availability Zones</li>
<li>An internet gateway (not shown in the diagram) associated with the public subnets</li>
<li>A NAT Gateway in one of the public subnets</li>
<li>An Amazon Relational Database Service (Amazon RDS) DB instance in one of the private subnets</li>
</ul>
<p>The following image shows the initial architecture:</p>

<p><img src="https://us-east-1-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-4-ha/instructions/en_us/images/starting.png" alt="Starting"></p>

<p>In this task, you will review the configuration of the VPC that has already been created.</p>
<ol start="4">
<li><p>In the AWS Management Console, on the <span style="background-color:#232f3e;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Services <i class="fas fa-angle-down"></i></span> menu, click <strong>VPC</strong>.</p></li>
<li><p>If you see <strong>New VPC Experience</strong> at the top-left of your screen, ensure <i class="fas fa-toggle-on"></i> <strong>New VPC Experience</strong> is selected. This lab is designed to use the new VPC Console.</p></li>
<li><p>In the left navigation pane, under <strong>Filter by VPC</strong>, click in the <i class="fas fa-search"></i> <strong>Select a VPC</strong> box, and select <em>Lab VPC</em>.</p></li>
</ol>
<p>This limits the console to only show resources associated with the Lab VPC.</p>
<ol start="7">
<li>In the left navigation pane, click <strong>Your VPCs</strong>.</li>
</ol>
<p>Here you can see the Lab VPC that was created for you.</p>
<ol start="8">
<li>In the left navigation pane, click <strong>Subnets</strong>.</li>
</ol>
<p>Here you can see the subnets that are part of the Lab VPC. For <strong>Public Subnet 1</strong>, look at the details in the columns:</p>
<ul>
<li>In the <strong>VPC</strong> column, you can see that this subnet exists inside of the <strong>Lab VPC</strong>.</li>
<li>In the <strong>IPv4 CIDR</strong> column, the value is <strong>10.0.0.0/24</strong>, which means this subnet includes the 256 IPs (5 of which are reserved and unusable) between 10.0.0.0 and 10.0.0.255.</li>
<li>In the <strong>Availability Zone</strong> column, you can see the Availability Zone in which this subnet resides.</li>
</ul><ol start="9">
<li>Select <i class="far fa-check-square"></i> <strong>Public Subnet 1</strong> to reveal more details at the bottom of the page.</li>
</ol>
<p><strong>Tip:</strong> To expand the lower window pane, drag the divider up and down.</p>
<ol start="10">
<li>On the lower half of the page, click the <strong>Route Table</strong> tab.</li>
</ol>
<p>Here you can see details about the routing for this subnet:</p>
<ul>
<li>The first entry specifies that traffic destined within the VPC's CIDR range (<strong>10.0.0.0/20</strong>) will be routed within the VPC (<strong>local</strong>).</li>
<li>The second entry specifies that any traffic destined for the internet (<strong>0.0.0.0/0</strong>) is routed to the internet gateway (<strong>igw-xxxx</strong>).  This setting makes it a <em>public</em> subnet.</li>
</ul><ol start="11">
<li>Click the <strong>Network ACL</strong> tab.</li>
</ol>
<p>Here you can see the network access control list (ACL) associated with the subnet. The rules currently permit <strong>ALL Traffic</strong> to flow in and out of the subnet. You can further restrict the traffic by using security groups.</p>
<ol start="12">
<li>In the left navigation pane, click <strong>Internet Gateways</strong>.</li>
</ol>
<p>Notice that an internet gateway is already associated with the Lab VPC.</p>
<ol start="13">
<li><p>In the left navigation pane, click <strong>Security Groups</strong>.</p></li>
<li><p>Select the <i class="far fa-check-square"></i> <strong>Inventory-DB</strong> security group.</p></li>
</ol>
<p>This is the security group used to control incoming traffic to the database.</p>
<ol start="15">
<li>On the lower half of the page, click the <strong>Inbound rules</strong> tab.</li>
</ol>
<p>Notice that the security group permits inbound MYSQL/Aurora traffic (port 3306) from anywhere within the VPC (<em>10.0.0.0/20</em>). You will later modify this to only accept traffic from the application servers.</p>
<ol start="16">
<li>Click the <strong>Outbound rules</strong> tab.</li>
</ol>
<p>By default, security groups allow all outbound traffic. However, you can modify these rules as necessary.</p>



<h2 id="step4">Task 2: Creating an Application Load Balancer</h2>

<p>To build a highly available application, it is best practice to launch resources in <em>multiple Availability Zones</em>. Availability Zones are physically separate data centers (or groups of data centers) within the same Region. Running your applications across multiple Availability Zones provides greater <em>availability</em> in case of failure within a data center.</p>

<p>When your application is running on multiple application servers, you need a way to distribute traffic among those servers. You can accomplish this by using a <em>load balancer</em>. A load balancer distributes incoming application traffic across multiple instances. A load balancer also performs health checks on instances and only sends requests to healthy instances.</p>

<p>The following diagram shows how an Application Load Balancer distributes incoming traffic to multiple application servers:</p>

<p><img src="https://us-east-1-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-4-ha/instructions/en_us/images/load-balancing.png" alt="Load Balancing"></p>

<p>In this task, you will create and configure an Application Load Balancer.</p>
<ol start="17">
<li><p>On the <span style="background-color:#232f3e;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Services <i class="fas fa-angle-down"></i></span> menu, click <strong>EC2</strong>.</p></li>
<li><p>If you see <strong>New EC2 Experience</strong> at the top-left of your screen, ensure <i class="fas fa-toggle-on"></i> <strong>New EC2 Experience</strong> is selected. This lab is designed to use the new EC2 Console.</p></li>
<li><p>In the left navigation pane, click <strong>Load Balancers</strong> (you may need to scroll down to find it).</p></li>
<li><p>Click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create Load Balancer</span></p></li>
</ol>
<p>Multiple load balancer types are displayed. Read the description of each type to understand its capabilities.</p>
<ol start="21">
<li><p>For <strong>Application Load Balancer</strong>, click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create</span></p></li>
<li><p>For <strong>Name</strong>, enter <input readonly class="copyable-inline-input" size="12" type="text" value="Inventory-LB"></p></li>
<li><p>In the <strong>Availability Zones</strong> section, for <strong>VPC</strong>, select <em>Lab VPC</em>.</p></li>
</ol>
<p>Now specify which <em>subnets</em> the load balancer should use. It will be an internet-facing load balancer, so select both public subnets.</p>
<ol start="24">
<li><p>Select the first displayed Availability Zone, and select the <em>Public Subnet</em> from the dropdown menu.</p></li>
<li><p>Select the second displayed Availability Zone, and select the <em>Public Subnet</em> from the dropdown menu.</p></li>
</ol>
<p>You should have two subnets selected: <strong>Public Subnet 1</strong> and <strong>Public Subnet 2</strong>. (If not, go back and try the configuration again.)</p>
<ol start="26">
<li>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next: Configure Security Settings</span>
</li>
</ol>
<p>A warning displays and recommends using HTTPS for improved security. This is good advice but is not necessary for this lab.</p>
<ol start="27">
<li>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next: Configure Security Groups</span>
</li>
</ol>
<p>Now create a security group that accepts all incoming HTTP and HTTPS traffic.</p>
<ol start="28">
<li>Select <i class="far fa-dot-circle"></i> <strong>Create a new security group</strong> and configure:</li>
</ol><ul>
<li>
<strong>Security group name:</strong> <input readonly class="copyable-inline-input" size="12" type="text" value="Inventory-LB">
</li>
<li>
<strong>Description:</strong> <input readonly class="copyable-inline-input" size="34" type="text" value="Enable web access to load balancer">
</li>
</ul><ol start="29">
<li>Configure the existing rule (already shown on the page) as follows:</li>
</ol><ul>
<li>
<strong>Type:</strong> <em>HTTP</em>
</li>
<li>
<strong>Source:</strong> <em>Anywhere</em>
</li>
</ul><ol start="30">
<li>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Add Rule</span> and configure:</li>
</ol><ul>
<li>
<strong>Type:</strong> <em>HTTPS</em>
</li>
<li>
<strong>Source:</strong> <em>Anywhere</em>
</li>
</ul>
<p>These settings will accept all incoming HTTP and HTTPS requests.</p>
<ol start="31">
<li>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next: Configure Routing</span>
</li>
</ol>
<p><em>Target groups</em> define where to <em>send</em> traffic that comes into the load balancer. The Application Load Balancer can send traffic to multiple target groups based on the URL of the incoming request. For example, requests from mobile apps could be sent to a different set of servers. For this lab, your web application will use only one target group.</p>
<ol start="32">
<li><p>For <strong>Name</strong>, enter <input readonly class="copyable-inline-input" size="13" type="text" value="Inventory-App"></p></li>
<li><p>Expand the <i class="fas fa-caret-right"></i> <strong>Advanced health check settings</strong> section.</p></li>
</ol>
<p>The Application Load Balancer automatically performs <em>health checks</em> on all instances to ensure that they are responding to requests. The default settings are recommended, but you will make them slightly faster for use in this lab.</p>
<ol start="34">
<li>Configure these values:</li>
</ol><ul>
<li>
<strong>Healthy threshold:</strong> <input readonly class="copyable-inline-input" size="1" type="text" value="2">
</li>
<li>
<strong>Interval:</strong> <input readonly class="copyable-inline-input" size="2" type="text" value="10">
</li>
</ul>
<p>This means that the health check will be performed every 10 seconds (<em>interval</em>). If the instance responds correctly twice in a row (<em>threshold</em>), it will be considered healthy.</p>
<ol start="35">
<li>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next: Register Targets</span>
</li>
</ol>
<p><em>Targets</em> are the individual instances that will respond to requests from the load balancer. You do not have any web application instances yet, so you can skip this step.</p>
<ol start="36">
<li><p>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next: Review</span></p></li>
<li><p>Review the settings. Then, click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create</span> and <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Close</span></p></li>
</ol>
<p>Your Application Load Balancer will now be provisioned in the background. You may continue to the next task without waiting.</p>



<p><i class="fas fa-info-circle"></i> Before you can create an Auto Scaling group using a launch template, you must create a launch template that includes the parameters required to launch an EC2 instance, such as the ID of the Amazon Machine Image (AMI) and an instance type.</p>

<p>In this task you will create a launch template.</p>
<ol start="38">
<li><p>In the <span style="background-color:#232f3e;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Services</span> menu, click <strong>EC2</strong>.</p></li>
<li><p>In the left navigation pane, below <strong>Instances</strong>, select <strong>Launch Templates</strong>.</p></li>
</ol>
<p><i class="fas fa-info-circle"></i> If a launch template already exists, select it, then select <strong>Delete template</strong> under <strong>Actions</strong>.</p>
<ol start="40">
<li><p>Select <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create launch template</span> then configure:</p></li>
<li><p>In the <strong>Launch template name and description</strong> section configure:</p></li>
</ol><ul>
<li>
<strong>Launch template name:</strong> <input readonly class="copyable-inline-input" size="19" type="text" value="Lab-template-NUMBER"> </li>
</ul>
<p><em>Note</em> - Relace <em>NUMBER</em> with a random number as shown below.</p>

<p>e.g. <em><input readonly class="copyable-inline-input" size="21" type="text" value="Lab-template-98469549"></em></p>

<p><i class="fas fa-info-circle"></i> If the template name already exists, try again with a different number.</p>
<ul>
<li>
<strong>Template version description:</strong> <input readonly class="copyable-inline-input" size="9" type="text" value="version 1">
</li>
</ul>
<p>You will be asked to select an <strong>Amazon Machine Image (AMI)</strong>, which is a template for the root volume of the instance and can contain an operating system, an application server and applications. You use an AMI to launch an <strong>instance</strong>, which is a copy of the AMI running as a virtual server in the cloud.</p>

<p>AMIs are available for various versions of Windows and Linux. In this lab, you will launch an instance running <em>Amazon Linux</em>.</p>
<ol start="42">
<li><p>For <strong>AMI</strong>, select <em>Amazon Linux 2 AMI</em>.</p></li>
<li><p>For <strong>Instance type</strong>, select <em>t3.micro</em>.</p></li>
</ol>
<p>When you launch an instance, the <strong>instance type</strong> determines the hardware allocated to your instance. Each instance type offers different compute, memory, and storage capabilities and are grouped in <strong>instance families</strong> based on these capabilities.</p>
<ol start="44">
<li><p>For <strong>Security groups</strong> select <em>Inventory-App</em>.</p></li>
<li><p>Scroll down to the <strong>Advanced Details</strong> section.</p></li>
<li><p>Expand <i class="fas fa-caret-right"></i> <strong>Advanced details</strong>.</p></li>
<li><p>For <strong>IAM instance profile:</strong> select <em>Inventory-App-Role</em>.</p></li>
<li><p>In the <strong>User data</strong> section, add:</p></li>
</ol><pre class="highlight plaintext"><code>#!/bin/bash&#x000A;# Install Apache Web Server and PHP&#x000A;yum install -y httpd mysql&#x000A;amazon-linux-extras install -y php7.2&#x000A;# Download Lab files&#x000A;wget https://us-west-2-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-2-webapp/scripts/inventory-app.zip&#x000A;unzip inventory-app.zip -d /var/www/html/&#x000A;# Download and install the AWS SDK for PHP&#x000A;wget https://github.com/aws/aws-sdk-php/releases/download/3.62.3/aws.zip&#x000A;unzip aws -d /var/www/html&#x000A;# Turn on web server&#x000A;chkconfig httpd on&#x000A;service httpd start&#x000A;</code></pre><ol start="49">
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create launch template</span></p></li>
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">View launch templates</span></p></li>
</ol>


<h2 id="step5">Task 3: Creating an Auto Scaling group</h2>

<p>Amazon EC2 Auto Scaling is a service designed to <em>launch</em> or <em>terminate</em> Amazon EC2 instances automatically based on user-defined policies, schedules, and health checks. The service also automatically distributes instances across multiple Availability Zones to make applications highly available.</p>

<p>In this task, you create an Auto Scaling group that deploys Amazon EC2 instances across your <em>private subnets</em>. This is a security best practice when deploying applications because instances in a private subnet cannot be accessed from the internet. Instead, users will send requests to the Application Load Balancer, which will forward the requests to Amazon EC2 instances in the private subnets, as shown in the following diagram:</p>

<p><img src="https://us-east-1-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-4-ha/instructions/en_us/images/load-balancing.png" alt="Load Balancing"></p>
<ol start="51">
<li><p>In the left navigation pane, below <strong>Auto Scaling</strong>, click <strong>Auto Scaling Groups</strong>.</p></li>
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create an Auto Scaling group</span> then configure:</p></li>
</ol><ul>
<li>
<strong>Name:</strong> <input readonly class="copyable-inline-input" size="13" type="text" value="Inventory-ASG">
</li>
<li>
<strong>Launch template:</strong> select the launch template that you created.</li>
<li>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next</span>
</li>
</ul><ol start="53">
<li>In the <strong>Network</strong> section, configure:</li>
</ol><ul>
<li>
<strong>VPC:</strong> <em>Lab VPC</em>
</li>
<li>
<strong>Subnets:</strong> select <em>Private Subnet 1 and Private Subnet 2</em>
</li>
</ul><ol start="54">
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next</span></p></li>
<li><p>On the <strong>Configure advanced options</strong> page, configure:</p></li>
</ol><ul>
<li>
<i class="far fa-check-square"></i> <strong>Enable load balancing</strong>
</li>
<li>
<strong>Choose a target group for your load balancer:</strong> Select <em>Inventory-App</em>
</li>
</ul>
<p>This tells the Auto Scaling group to register new EC2 instances as part of the <em>Inventory-App</em> target group that you created earlier. The load balancer will send traffic to instances that are in this target group.</p>
<ul>
<li>
<strong>Health check grace period:</strong> <input readonly class="copyable-inline-input" size="3" type="text" value="200">
</li>
<li>
<strong>Monitoring:</strong> <i class="far fa-check-square"></i> <em>Enable group metrics collection within CloudWatch</em>
</li>
<li>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next</span>
</li>
</ul>
<p>By default, the health check grace period is set to 300. Since this is a lab environment, you have set it to 200 to avoid having to wait very long to see auto scaling perform the first health check.</p>
<ol start="56">
<li>On the <strong>Configure group size and scaling policies</strong> page, configure:</li>
</ol><ul>
<li>
<strong>Desired capacity:</strong> <input readonly class="copyable-inline-input" size="1" type="text" value="2">
</li>
<li>
<strong>Minimum capacity:</strong> <input readonly class="copyable-inline-input" size="1" type="text" value="2">
</li>
<li>
<strong>Maximum capacity:</strong> <input readonly class="copyable-inline-input" size="1" type="text" value="2">
</li>
<li>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next</span>
</li>
</ul>
<p>For this lab, you will maintain two instances at all times to ensure high availability. If the application is expected to receive varying loads of traffic, it is also possible to create <em>scaling policies</em> that define when to launch/terminate instances. However, this is not necessary for the Inventory application in this lab.</p>
<ol start="57">
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next</span> until you get to the <strong>Tags</strong> page.</p></li>
<li><p>Click <span style="background-color:white;font-weight:bold;font-size:90%;color:#545b64;border-color:#545b64;border-radius:2px;border-width:1px;border-style:solid;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Add tag</span> then configure:</p></li>
</ol><ul>
<li>
<strong>Key:</strong> <input readonly class="copyable-inline-input" size="4" type="text" value="Name">
</li>
<li>
<strong>Value:</strong> <input readonly class="copyable-inline-input" size="13" type="text" value="Inventory-App">
</li>
</ul>
<p>This tags the Auto Scaling group with a name, which will also appear on the EC2 instances that the Auto Scaling group launches. This makes it easier to identify which EC2 instances are associated with which application. You could also add tags such as Cost Center to make it easier to assign application costs in billing files.</p>
<ol start="59">
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Next</span></p></li>
<li><p>Review the Auto Scaling group configuration, then click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create Auto Scaling group</span></p></li>
</ol>
<p>Your application will soon be running across two Availability Zones, and Auto Scaling will maintain that configuration even if an instance or Availability Zone fails.</p>

<p>Now that you have created your Auto Scaling group, you can verify that the group has launched your EC2 instance.</p>
<ol start="61">
<li>Click on your Auto Scaling Group.</li>
</ol>
<p>Examine the <strong>Group Details</strong> to view information about the Auto Scaling group.</p>
<ol start="62">
<li>Click the <strong>Activity</strong> tab.</li>
</ol>
<p>The Status column contains the current status of your instances. When your instances are launching, the status column shows <em>PreInService</em>. The status changes to <em>Successful</em> once an instance is launched. You can click the refresh <i class="fas fa-sync"></i> button to see the current status of your instance.</p>
<ol start="63">
<li>Click the <strong>Instance management</strong> tab.</li>
</ol>
<p>You can see that your Auto Scaling group has launched your EC2 instances and they are in the <em>InService</em> lifecycle state. The Health Status column shows the result of the EC2 instance health check on your instances.</p>
<ol start="64">
<li>Click the <strong>Monitoring</strong> tab. Here you can see monitoring related info for your Autoscaling group.</li>
</ol>


<h2 id="step6">Task 4: Updating security groups</h2>

<p>The application you have deployed has a <em>three-tier architecture</em>. In this task, you will configure the security groups to enforce these tiers, as shown in the following image:</p>

<p><img src="https://us-east-1-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-4-ha/instructions/en_us/images/security.png" alt="Security"></p>

<h3>Load balancer security group</h3>

<p>You already configured the load balancer security group when you created the Application Load Balancer. This security group accepts all incoming HTTP and HTTPS traffic.</p>

<p>The load balancer is configured to forward incoming requests to a target group. When Auto Scaling launches new instances, it will automatically add those instances to the target group.</p>

<h3>Application security group</h3>

<p>The application security group was provided as part of the lab setup. Now, configure it to only accept incoming traffic from the load balancer.</p>
<ol start="65">
<li><p>In the left navigation pane, click <strong>Security Groups</strong>.</p></li>
<li><p>Select <i class="far fa-check-square"></i> <strong>Inventory-App</strong> (and make sure no other security groups are selected).</p></li>
<li><p>On the lower half of the page, click the <strong>Inbound rules</strong> tab.</p></li>
</ol>
<p>The security group is currently empty. You will add a rule to accept incoming HTTP traffic from the load balancer. There is no need to configure HTTPS traffic because the load balancer has been configured to forward HTTPS requests via HTTP. This off-loads security to the load balancer, reducing the amount of work required by the individual application servers.</p>
<ol start="68">
<li><p>Click <span style="background-color:white;font-weight:bold;font-size:90%;color:#545b64;border-color:#545b64;border-radius:2px;border-width:1px;border-style:solid;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Edit inbound rules</span></p></li>
<li><p>Click <span style="background-color:white;font-weight:bold;font-size:90%;color:#545b64;border-color:#545b64;border-radius:2px;border-width:1px;border-style:solid;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Add rule</span> and configure:</p></li>
</ol><ul>
<li>
<strong>Type:</strong> <em>HTTP</em>
</li>
<li>
<strong>Source:</strong>
<ul>
<li>In the box to the right of <strong>Custom</strong>, type <input readonly class="copyable-inline-input" size="2" type="text" value="sg">
</li>
<li>Select <em>Inventory-LB</em> from the list that appears</li>
</ul>
</li>
<li>
<strong>Description:</strong> <input readonly class="copyable-inline-input" size="26" type="text" value="Traffic from load balancer">
</li>
</ul><ol start="70">
<li>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Save rules</span>
</li>
</ol>
<p>The application servers can now receive traffic from the load balancer. This includes health checks that the load balancer automatically performs.</p>

<h3>Database security group</h3>

<p>Now, configure the database security group to only accept incoming traffic from the application servers.</p>
<ol start="71">
<li>Select <i class="far fa-check-square"></i> <strong>Inventory-DB</strong> (and make sure no other security groups are selected).</li>
</ol>
<p>The existing inbound rule permits traffic on port 3306 (used by MySQL) from any IP address within the VPC. This is a good rule, but the security can be tightened further.</p>
<ol start="72">
<li>On the <strong>Inbound rules</strong> tab, click <span style="background-color:white;font-weight:bold;font-size:90%;color:#545b64;border-color:#545b64;border-radius:2px;border-width:1px;border-style:solid;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Edit inbound rules</span> and configure:</li>
</ol><ul>
<li>
<strong>Source:</strong>
<ul>
<li>Remove the <strong>10.0.0.0/20</strong> source</li>
<li>In the box to the right of <strong>Custom</strong>, type <input readonly class="copyable-inline-input" size="2" type="text" value="sg">
</li>
<li>Select <em>Inventory-App</em> from the list that appears</li>
</ul>
</li>
<li>
<strong>Description:</strong> <input readonly class="copyable-inline-input" size="24" type="text" value="Traffic from app servers">
</li>
</ul><ol start="73">
<li>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Save rules</span>
</li>
</ol>
<p>You have now configured three-tier security, with each element in a tier only accepting traffic from the tier above.</p>

<p>In addition, the use of private subnets means that there are two security barriers between the internet and your application resources. This matches the best practice of applying multiple layers of security.</p>



<h2 id="step7">Task 5: Testing the application</h2>

<p>Your application is now ready for testing. In this task, confirm that your web application is running and highly available.</p>
<ol start="74">
<li><p>In the left navigation pane, click <strong>Target Groups</strong>.</p></li>
<li><p>Under <strong>Name</strong>, click <em>Inventory-App</em></p></li>
<li><p>On the lower half of the page, click the <strong>Targets</strong> tab.</p></li>
</ol>
<p>In the <strong>Registered targets</strong> section, you should see two instances. The <strong>Status</strong> column shows the results of the load balancer health check that was performed against the instances.</p>
<ol start="77">
<li>Click the refresh <i class="fas fa-sync"></i> icon at the top-right of the page every few seconds until the <strong>Status</strong> for both instances appears as <em>healthy</em>.</li>
</ol>
<p>If the status does not eventually change to <em>healthy</em>, ask your instructor for assistance in diagnosing the configuration. Hovering on the information <i class="fas fa-info-circle"></i> icon in the <strong>Status</strong> column provides more information about the status.</p>

<p>You will test the application by connecting to the Application Load Balancer, which will send your request to one of the Amazon EC2 instances. First, you need to retrieve the DNS name of the Application Load Balancer.</p>
<ol start="78">
<li><p>In the left navigation pane, click <strong>Load Balancers</strong>.</p></li>
<li><p>In the <strong>Description</strong> tab on the lower half of the page, copy the <strong>DNS name</strong> to your clipboard.</p></li>
</ol>
<p>It should be similar to: <em>Inventory-LB-xxxx.elb.amazonaws.com</em></p>
<ol start="80">
<li>Open a new web browser tab, paste the DNS name from your clipboard, and press ENTER.</li>
</ol>
<p>The load balancer forwards your request to one of the Amazon EC2 instances. The bottom of the web page displays the instance ID and Availability Zone.</p>
<ol start="81">
<li>Refresh the page in your web browser a few times. You should notice that the instance ID and Availability Zone sometimes changes between the two instances.</li>
</ol>
<p>The following image displays the flow of information for this web application:</p>

<p><img src="https://us-east-1-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-4-ha/instructions/en_us/images/request-flow.png" alt="Request flow"></p>

<p>The flow of information is as follows:</p>
<ul>
<li>You sent the request to the Application Load Balancer, which resides in the <em>public</em> subnets. The public subnets are connected to the internet.</li>
<li>The Application Load Balancer chose one of the Amazon EC2 instances that reside in the <em>private</em> subnets and forwarded the request to the instance.</li>
<li>The Amazon EC2 instance then returned the web page to the Application Load Balancer, which returned the page to your web browser.</li>
</ul>


<h2 id="step8">Task 6: Testing high availability</h2>

<p>Your application is now configured to be highly available. You can test this by terminating one of the Amazon EC2 instances.</p>
<ol start="82">
<li><p>Return to the <strong>EC2 Management Console</strong> but do not close the application tab. (You will return to it soon.)</p></li>
<li><p>In the left navigation pane, click <strong>Instances</strong>.</p></li>
</ol>
<p>Now, you will terminate one of the web application instances to simulate a failure.</p>
<ol start="84">
<li><p>Select one of the <strong>Inventory-App</strong> instances. (It does not matter which one you select.)</p></li>
<li><p>Click <span style="background-color:white;font-weight:bold;font-size:90%;color:#545b64;border-color:#545b64;border-radius:2px;border-width:1px;border-style:solid;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Actions <i class="fas fa-angle-down"></i></span> and then <strong>Instance State &gt; Terminate instance</strong>.</p></li>
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Terminate</span></p></li>
</ol>
<p>In a short time, the load balancer health checks will notice that the instance is not responding and will automatically route all requests to the remaining instance.</p>
<ol start="87">
<li>Return to the Inventory application tab in your web browser and refresh the page several times.</li>
</ol>
<p>You should notice that the Availability Zone shown at the bottom of the page stays the same. Even though an instance has failed, your application remains available.</p>

<p>After a few minutes, Auto Scaling will also notice the instance failure. You configured Auto Scaling to keep two instances running, so Auto Scaling will automatically launch a replacement instance.</p>
<ol start="88">
<li>Return to the EC2 Management Console. Click the refresh <i class="fas fa-sync"></i> icon at the top-right of the page every 30 seconds until a new Amazon EC2 instance appears.</li>
</ol>
<p>After a few minutes, the health check for the new instance should become healthy, and the load balancer will continue sending traffic between two Availability Zones.</p>
<ol start="89">
<li>Return to the Inventory application tab and refrsh the page several times. You will see the instance Id change as you refresh the page.</li>
</ol>
<p>This demonstrates that your application is now highly available.</p>

<h2 id="step9">Challenge: Making the database highly available</h2>

<p><i class="fas fa-comment"></i> <strong>Note</strong> This challenge task is <strong>optional</strong> and is provided in case you have lab time remaining. To skip to the end of the lab, <a href="#conclusion" target="_blank">click here</a>.</p>

<p>The application architecture is now highly available. However, the Amazon RDS database is still operating from only one database instance.</p>

<p>In this task, you will make the database highly available by configuring it to run across multiple Availability Zones ("multi-AZ").</p>
<ol start="90">
<li><p>In the AWS Management Console, on the <span style="background-color:#232f3e;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Services <i class="fas fa-angle-down"></i></span> menu, click <strong>RDS</strong>.</p></li>
<li><p>In the left navigation pane, click <strong>Databases</strong>.</p></li>
<li><p>Click the <strong>inventory-db</strong> identifier.</p></li>
<li><p>Click <span style="background-color:white;font-weight:bold;font-size:90%;color:#545b64;border-color:#545b64;border-radius:2px;border-width:1px;border-style:solid;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Modify</span></p></li>
<li><p>For <strong>DB instance class</strong>, select <strong>db.t3.small</strong>.</p></li>
</ol>
<p>This will double the size of the instance.</p>
<ol start="95">
<li>For <strong>Allocated storage</strong>, enter <input readonly class="copyable-inline-input" size="2" type="text" value="10">
</li>
</ol>
<p>This will double the amount of space allocated to the database.</p>

<p>Feel free to review the other options on the page, but do not change any of the values.</p>
<ol start="96">
<li>For <strong>Multi-AZ deployment</strong>, select <i class="far fa-dot-circle"></i> <strong>Create a standby instance (recommended for production usage)</strong>.</li>
</ol>
<p>This is the only selection necessary to convert the database to run across multiple data centers (Availability Zones).</p>

<p>Note that this does not mean that the database is <em>distributed</em> across multiple instances. Rather, one instance is the <em>primary</em> and is handling all requests. Another instance will be launched as the <em>secondary</em> instance and will take over if the primary fails. Your application continues to use the same DNS name for the database, but the connections will automatically redirect to the currently active database server.</p>

<p>Just as it is possible to scale up an Amazon EC2 instance by changing its attributes, it is possible to scale an Amazon RDS database instance. You will now scale up the database.</p>
<ol start="97">
<li>At the bottom of the page, click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Continue</span>
</li>
</ol>
<p>Notice the warning about the potential performance impact from these changes. Because of the performance impact, you can schedule the changes to occur during the next scheduled maintenance window or immediately.</p>
<ol start="98">
<li><p>In the <strong>Scheduling of modifications</strong> section, select <i class="far fa-dot-circle"></i> <strong>Immediately</strong>.</p></li>
<li><p>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Modify DB Instance</span></p></li>
</ol>
<p>The database enters a <em>Modifying</em> state while the changes are applied. You may continue to the next task without waiting.</p>

<h2 id="step10">Challenge: Making the NAT Gateway highly available</h2>

<p><i class="fas fa-comment"></i> <strong>Note</strong> This challenge task is <strong>optional</strong> and is provided in case you have lab time remaining. To skip to the end of the lab, <a href="#conclusion" target="_blank">click here</a>.</p>

<p>The application servers are running in a private subnet. If they need to access the internet (for example to download data), the requests must be redirected through a <em>NAT Gateway</em> (located in a public subnet).</p>

<p>The current architecture has only one NAT Gateway in Public Subnet 1. This means that if Availability Zone 1 failed, the application servers would not be able to communicate with the internet.</p>

<p>In this challenge, you will make the NAT Gateway highly available by launching another NAT Gateway in the other Availability Zone.</p>

<p>The resulting architecture, shown in the following diagram, will be highly available:</p>

<p><img src="https://us-east-1-tcprod.s3.amazonaws.com/courses/ILT-TF-200-ARCHIT/v6.8.12/lab-4-ha/instructions/en_us/images/architecture.png" alt="Architecture"></p>
<ol start="100">
<li><p>On the <span style="background-color:#232f3e;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Services <i class="fas fa-angle-down"></i></span> menu, click <strong>VPC</strong>.</p></li>
<li><p>In the left navigation pane, click <strong>NAT Gateways</strong>.</p></li>
</ol>
<p>The existing NAT Gateway is displayed. Now create one for the other Availability Zone.</p>
<ol start="102">
<li>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create NAT gateway</span> and configure:</li>
</ol><ul>
<li>
<strong>Name:</strong> <input readonly class="copyable-inline-input" size="14" type="text" value="my-nat-gateway">
</li>
<li>
<strong>Subnet:</strong> Select the subnet that is shown to the left of these instructions as <strong>PublicSubnet2</strong>
</li>
<li>Click <span style="background-color:white;font-weight:bold;font-size:90%;color:#545b64;border-color:#545b64;border-radius:2px;border-width:1px;border-style:solid;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">Allocate Elastic IP address</span>
</li>
<li>Click <span style="background-color:#ec7211;font-weight:bold;font-size:90%;color:white;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create NAT gateway</span>
</li>
</ul>
<p>Now, create a new route table for Private Subnet 2 that redirects traffic to the new NAT Gateway.</p>
<ol start="103">
<li><p>In the left navigation pane, click <strong>Route Tables</strong>.</p></li>
<li><p>Click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create route table</span> and configure:</p></li>
</ol><ul>
<li>
<strong>Name tag:</strong> <input readonly class="copyable-inline-input" size="21" type="text" value="Private Route Table 2">
</li>
<li>
<strong>VPC:</strong> <em>Lab VPC</em>
</li>
</ul><ol start="105">
<li><p>Click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Create</span> and then click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Close</span></p></li>
<li><p>Select <i class="far fa-check-square"></i> <strong>Private Route Table 2</strong>, ensuring that it is the only route table selected.</p></li>
<li><p>Click the <strong>Routes</strong> tab.</p></li>
</ol>
<p>There is currently one route, which directs all traffic <em>locally</em>.</p>

<p>Now, add a route to send internet-bound traffic through the new NAT Gateway.</p>
<ol start="108">
<li><p>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Edit routes</span></p></li>
<li><p>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Add route</span> and configure:</p></li>
</ol><ul>
<li>
<strong>Destination:</strong> <input readonly class="copyable-inline-input" size="9" type="text" value="0.0.0.0/0">
</li>
<li>
<strong>Target:</strong> Select <em>NAT Gateway</em> &gt; <em>my-nat-gateway</em>
</li>
<li>Click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Save routes</span> and then click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Close</span>
</li>
</ul>
<p><i class="fas fa-comment"></i> <strong>Note</strong> The NAT Gateway shown to the left of these instructions is for Public Subnet 1. You are configuring the route table to use the <em>other</em> NAT Gateway.</p>
<ol start="110">
<li><p>Click the <strong>Subnet Associations</strong> tab.</p></li>
<li><p>Click <span style="background-color:#DEDEDE;font-weight:bold;font-size:90%;color:#444;border-radius:5px;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Edit subnet associations</span></p></li>
<li><p>Select <i class="far fa-check-square"></i> <strong>Private Subnet 2</strong>.</p></li>
<li><p>Click <span style="background-color:#257ACF;font-weight:bold;font-size:90%;color:white;border-radius:5px;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;white-space: nowrap;">Save</span></p></li>
</ol>
<p>Internet-bound traffic from Private Subnet 2 will now be sent to the NAT Gateway that is in the same Availability Zone.</p>

<p>Your NAT Gateways are now highly available. A failure in one Availability Zone will not impact traffic in the other Availability Zone.</p>

<h2 id="step11">Conclusion</h2>

<p>Congratulations! You now have successfully:</p>
<ul>
<li>Created an Application Load Balancer</li>
<li>Created an Amazon EC2 Auto Scaling group</li>
<li>Updated security groups to enforce a three-tier architecture</li>
</ul>
<h2 id="step12">End Lab</h2>

<p>Follow these steps to close the console, end your lab, and evaluate the experience.</p>
<ol start="114">
<li><p>Return to the AWS Management Console.</p></li>
<li><p>On the navigation bar, choose <strong>awsstudent@&lt;AccountNumber&gt;</strong>, and then choose <strong>Sign Out</strong>.</p></li>
<li><p>Choose <span style="background-color:#D93025;font-family:Google Sans;font-weight:bold;font-size:90%;color:white;border-color:#D93025;border-radius:4px;border-width:2px;border-style:solid;padding-top:5px;padding-bottom:5px;padding-left:10px;padding-right:10px;">End Lab</span></p></li>
<li><p>Choose <span style="background-color:#DEDEDE;font-family:Google Sans;font-weight:bold;font-size:90%;color:#444;border-width:1px;border-style:solid;border-color:#444;padding-top:3px;padding-bottom:3px;padding-left:10px;padding-right:10px;">OK</span></p></li>
<li><p>(Optional):</p></li>
</ol><ul>
<li>Select the applicable number of stars <i class="far fa-star"></i>
</li>
<li>Type a comment</li>
<li>
<p>Choose <strong>Submit</strong></p>
<ul>
<li>1 star = Very dissatisfied</li>
<li>2 stars = Dissatisfied</li>
<li>3 stars = Neutral</li>
<li>4 stars = Satisfied</li>
<li>5 stars = Very satisfied</li>
</ul>
</li>
</ul>
<p>You may close the window if you don't want to provide feedback.</p>

<h2 id="step13">Additional Resources</h2>

<p>For more information about AWS Training and Certification, see <a href="http://aws.amazon.com/training/" target="_blank"><em>http://aws.amazon.com/training/</em></a>.</p>

<p><em>Your feedback is welcome and appreciated.</em></p>

<p>If you would like to share any feedback, suggestions, or corrections, please provide the details in our <a href="https://support.aws.amazon.com/#/contacts/aws-training" target="_blank"><em>AWS Training and Certification Contact Form</em></a>.</p>

</div>
</div>


<div class='hidden js-end-lab-button-container lab-content__end-lab-button'>
<ql-lab-control-button class='js-end-lab-button' running></ql-lab-control-button>
</div>
<!-- / TODO: Move recommendations into the end lab modal -->
</ql-drawer-content>
<ql-drawer end id='outline-drawer' open slot='drawer' width='320'>
<div class='js-lab-content-outline lab-content__outline'>
<a href='#step1'>Lab overview</a><a href='#step2'>Start Lab</a><a href='#step3'>Task 1: Inspecting your VPC</a><a href='#step4'>Task 2: Creating an Application Load Balancer</a><a href='#step5'>Task 3: Creating an Auto Scaling group</a><a href='#step6'>Task 4: Updating security groups</a><a href='#step7'>Task 5: Testing the application</a><a href='#step8'>Task 6: Testing high availability</a><a href='#step9'>Challenge: Making the database highly available</a><a href='#step10'>Challenge: Making the NAT Gateway highly available</a><a href='#step11'>Conclusion</a><a href='#step12'>End Lab</a><a href='#step13'>Additional Resources</a>
</div>
</ql-drawer>
</ql-drawer-container>
</ql-drawer-content>
</ql-drawer-container>
<div class='lab-introduction js-lab-introduction is-hidden'>
<div class='lab-introduction__inner'>
<h1 class='headline-1'>Welcome to Your First Lab!</h1>
<ql-icon-button class='js-skip-button'>close</ql-icon-button>
<div class='lab-introduction__video'>
<iframe allow='autoplay; encrypted-media' allowfullscreen frameborder='0' id='lab-introduction' src='https://www.youtube.com/embed/yF7EDXKTmoQ?enablejsapi=1&amp;rel=0&amp;showinfo=0'></iframe>
</div>
<a class='js-skip-button button button--outline'>Skip this video</a>
</div>
</div>



</div>
</main>
<div class='modal fade' id='lab-details-modal'>
<div class='modal-container'>
<div class='mdl-shadow--24dp modal-content'>
<div class='modal-body'>
<p class='l-mbm'>
In this lab, you will start with an application running on a single Amazon EC2 instance and will then convert it to be Highly Available.
</p>
<p class='small-label l-mbs'>
<strong>
Duration:
</strong>
0m setup
&middot;
180m access
&middot;
180m completion
</p>
<p class='small-label l-mbs'>
<strong>AWS Region:</strong>
[eu-west-1] <strong>EU (Ireland)</strong>
</p>
<p class='small-label l-mbs'>

</p>
<p class='small-label'>
<strong>
Permalink:
</strong>
<a href="https://informator.qwiklabs.com/catalog_lab/4419">https://informator.qwiklabs.com/catalog_lab/4419</a>
</p>
</div>
<div class='modal-actions'>
<a class='button button--text' data-dismiss='modal'>
Got It
</a>
</div>


</div>
</div>
<iframe class='l-ie-iframe-fix'></iframe>
</div>
<div class='modal fade' id='lab-review-modal'>
<div class='modal-container'>
<div class='mdl-shadow--24dp modal-content'>
<form class="simple_form js-lab-review-form" id="new_lab_review" action="/lab_reviews" accept-charset="UTF-8" data-remote="true" method="post"><input name="utf8" type="hidden" value="&#x2713;" /><div class='modal-body'>
<p class='label'>
How satisfied are you with this lab?*
</p>
<div class='rateit js-rateit' data-rateit-max='5' data-rateit-min='0' data-rateit-resetable='false' data-rateit-step='1' data-rateit-value='0'></div>
<div class='l-mtm'>

<div class="control-group hidden lab_review_user_id"><div class="controls"><input class="hidden" type="hidden" value="332" name="lab_review[user_id]" id="lab_review_user_id" /></div></div>
<div class="control-group hidden lab_review_classroom_id"><div class="controls"><input class="hidden" type="hidden" value="51" name="lab_review[classroom_id]" id="lab_review_classroom_id" /></div></div>
<div class="control-group hidden lab_review_lab_id"><div class="controls"><input class="hidden" type="hidden" value="4419" name="lab_review[lab_id]" id="lab_review_lab_id" /></div></div>
<div class="control-group hidden lab_review_focus_id"><div class="controls"><input class="hidden" type="hidden" value="352" name="lab_review[focus_id]" id="lab_review_focus_id" /></div></div>
<div class="control-group hidden lab_review_rating"><div class="controls"><input class="hidden js-rating-input" type="hidden" name="lab_review[rating]" id="lab_review_rating" /></div></div>
<div class="control-group text optional lab_review_comment"><label class="text optional control-label" for="lab_review_comment">Comment</label><div class="controls"><textarea class="text optional" name="lab_review[comment]" id="lab_review_comment">
</textarea></div></div>
</div>
</div>
<div class='modal-actions'>
<a class='button button--text' data-dismiss='modal'>
Cancel
</a>
<input type="submit" name="commit" value="Submit" disabled="disabled" id="submit" data-disabled="false" class="button" data-disable-with="Submit" />
</div>
</form>

</div>
</div>
<iframe class='l-ie-iframe-fix'></iframe>
</div>

<script>
  $( function() {
    ql.initMaterialInputs();
    initChosen();
    initSearch();
    initTabs();
    ql.list.init();
    ql.favoriting.init();
    ql.header.myAccount.init();
    initTooltips();
    ql.autocomplete.init();
    ql.modals.init();
    ql.toggleButtons.init();
    ql.analytics.init();
    initLabContent();
  ql.labOutline.links.init();
  initLabReviewModal();
  ql.labAssessment.init();
  ql.labData.init();
  initLabTranslations( {"are_you_sure":"All done? If you end this lab, you will lose all your work. You may not be able to restart the lab if there is a quota limit. Are you sure you want to end this lab?\n","in_progress":"*In Progress*","ending":"*Ending*","starting":"*Starting, please wait*","end_concurrent_labs":"Sorry, you can only run one lab at a time. To start this lab, please confirm that you want all of your existing labs to end.\n","copied":"Copied","no_resource":"Error retrieving resource.","no_support":"No Support","mac_press":"Press ⌘-C to copy","thanks_review":"Thanks for reviewing this lab.","windows_press":"Press Ctrl-C to copy","days":"days"} );
  ql.labRun.init();
  ql.chat.init();
  ql.initHeader();
  ql.navigation.init();
  ql.navPanel.init();
  ql.navigation.init();
  
  });
</script>
<style>
  .mdl-layout__container {
    position: static
  }
</style>
</body>
</html>

