Architecture Diagrams with Amazon Q CLI & MCP

INSTALLATION

WSL (Windows Subsystem For Linux)
Download installation zip file:
curl --proto '=https' --tlsv1.2 -sSf "https://desktop-release.q.us-east-1.amazonaws.com/latest/q-x86_64-linux.zip" -o "q.zip"
Unzip the installer:unzip q.zip
Run the install program:./q/install.shBy default, the files are installed to ~/.local/bin.

Linux (Ubuntu)
Make sure your machine is updated and has Libfuse2 installed
sudo apt-get update
sudo apt install libfuse2
Install the deb file for Amazon Q
curl --proto '=https' --tlsv1.2 -sSf https://desktop-release.q.us-east-1.amazonaws.com/latest/amazon-q.deb -o amazon-q.deb

Install Amazon Q debian file
sudo apt install -y ./amazon-q.deb
q login
? Select Login Method
> Use For Free for Builder Id
> Use with Pro License

Create Builder Id
https://community.aws/ # use it to sign in with Builder Id 

once you have logged in, just write simple command
q

MCP Support on Amazon Q CLI
Now let's power up your Amazon Q CLI with MCP Servers.
MCP Servers can be setup locally with npx , uvx, docker
In this blog we have used uvx

If you want to install simply use the commands
MacOS
brew install uv

Linux / WSL
sudo snap install astral-uv --classic

Now create a file called mcp.json in ~/.aws/amazonq
and add this ## For awslab mcp-server and aws-diagram-mcp-server

'''{

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

}'''

Now run q again


## Now write prompt according to the architecture you want to design and Amazon Q cli will create it for you.
