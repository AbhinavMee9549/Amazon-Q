Architecture Diagrams with Amazon Q CLI & MCP

INSTALLATION

<P> WSL (Windows Subsystem For Linux) </p>
<p> Download installation zip file: </p>  
<pre> 
curl --proto '=https' --tlsv1.2 -sSf "https://desktop-release.q.us-east-1.amazonaws.com/latest/q-x86_64-linux.zip" -o "q.zip"
Unzip the installer:unzip q.zip
Run the install program:./q/install.shBy default, the files are installed to ~/.local/bin.  
</pre>

<P>Linux (Ubuntu)</p>
Make sure your machine is updated and has Libfuse2 installed
<pre>
sudo apt-get update
sudo apt install libfuse2 </pre>
Install the deb file for Amazon Q
<pre> curl --proto '=https' --tlsv1.2 -sSf https://desktop-release.q.us-east-1.amazonaws.com/latest/amazon-q.deb -o amazon-q.deb </pre>


Install Amazon Q debian file
<pre>
sudo apt install -y ./amazon-q.deb
</pre>
<pre>
q login
</pre>
? Select Login Method
> Use For Free for Builder Id
> Use with Pro License

Create Builder Id
https://community.aws/ # use it to sign in with Builder Id 

once you have logged in, just write simple command
<pre> q </pre>

MCP Support on Amazon Q CLI
<p> Now let's power up your Amazon Q CLI with MCP Servers. </p>
<p> MCP Servers can be setup locally with npx , uvx, docker </p>
<p> In this blog we have used uvx </p>

If you want to install simply use the commands
<p> MacOS </p>
<pre> brew install uv </pre>

<p> Linux / WSL </p>
<pre> sudo snap install astral-uv --classic </pre>

<p> Now create a file called mcp.json in ~/.aws/amazonq </p>
<p> and add this   ## For awslab mcp-server and aws-diagram-mcp-server </p>
<pre>
{
    "mcpServers" : {
    
    
"awslabs.cdk-mcp-server": {
        "command": "uvx",
        "args": ["awslabs.cdk-mcp-server@latest"],
        "env": {
           "FASTMCP_LOG_LEVEL": "ERROR"
        }
   },
   
 "awslabs.aws-diagram-mcp-server": {
 		"command": "uvx",
 		"args": ["awslabs.aws-diagram-mcp-server"],
 		"env": {
 			"FASTMCP_LOG_LEVEL": "ERROR"
 		},
 		"autoApprove": [],
 		"disabled": false
 	}
}

}
</pre>




Now run q again


## Now write prompt according to the architecture you want to design and Amazon Q cli will create it for you.

#PROMPTS:

<p>First</p>
<pre>Build an AWS diagram where the backend application uploads files to S3, triggering a Lambda function to process metadata and store it in DynamoDB. Include SNS for optional notifications and use IAM roles with least privilege.
</pre>

<p>Second</p>
<pre>Design a CI/CD pipeline architecture where the backend application is deployed on EC2 via CodePipeline and CodeDeploy, while a separate data fetcher component is built and deployed to AWS Lambda. Add monitoring with CloudWatch and notifications via SNS.
</pre>

<p>Third</p>
<pre>Create a secure AWS architecture where a backend application encrypts files using KMS and stores them in a private S3 bucket. A data fetcher hosted in a different VPC accesses these files securely using VPC endpoints and IAM roles. Add GuardDuty and Config for compliance monitoring.
</pre>

<p>Fourth</p>
<pre>Design a simple AWS architecture where a backend service is hosted on an EC2 instance inside a private subnet, and a separate client component running on another EC2 instance retrieves data from it over HTTP. Use appropriate VPC, subnets, security groups, and IAM roles.
</pre> 

<p>Fifth</p>
<pre>Build an architecture where a distributed backend service is deployed across multiple AZs behind an ALB. Remote agents (polling services) deployed in separate environments periodically fetch job details and submit processed data back. Use DynamoDB for job queues and S3 for data exchange.
</pre>

<p>Sixth</p>
<pre>Generate a full-stack AWS architecture where the backend API is deployed via ECS Fargate, frontend is served through S3 + CloudFront, and a scheduled background function (Lambda) consumes the backend API and stores logs in CloudWatch.
</pre>
