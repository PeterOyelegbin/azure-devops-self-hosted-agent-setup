# Azure DevOps Self-Hosted Agent Setup
Steps to install a small agent on your VM (the CI/CD server) that listens for jobs from your Azure DevOps pipeline.

1. In your Azure DevOps project, go to `Project Settings`
   <img width="1916" height="821" alt="image" src="https://github.com/user-attachments/assets/dc482688-68b5-417d-acf7-241f219520de" />
2. Select `Agent Pools` > click `Add Pool`
   <img width="1919" height="826" alt="image" src="https://github.com/user-attachments/assets/b549e520-9a8b-43ac-840a-4302326d84e4" />
3. Create a new pool;
   ```
   Self-hosted: Select
   Naem: My-Lab-VMs
   Grant access permission to all pipelines: Enable
   ```
   <img width="1919" height="834" alt="image" src="https://github.com/user-attachments/assets/683be803-fc8c-478c-a5de-2179d9b2f697" />
4. SSH into your VM and follow Microsoft's guide to [install and configure the self-hosted agent](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/linux-agent?view=azure-devops&tabs=IP-V4). This involves downloading a script and running it, or running the command below;
   ```
   mkdir myagent && cd myagent
   wget https://download.agent.dev.azure.com/agent/4.261.0/vsts-agent-linux-x64-4.261.0.tar.gz
   tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz
   ./config.sh
   sudo ./svc.sh install
   sudo ./svc.sh start
   sudo ./svc.sh status
   ```
   Note:
     - Server URL = https://dev.azure.com/{your-organization}

5. Install the required Runtime on the VM (e.g, .NET, Node), adjust version as needed;
   ```
   # Install .NET 9.0 SDK
   wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
   sudo dpkg -i packages-microsoft-prod.deb
   rm packages-microsoft-prod.deb
   sudo apt-get update
   sudo apt-get install -y dotnet-sdk-9.0
   dotnet --version
   dotnet --list-sdks

   # Install Node.js (using Node Version Manager is best)
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
   # Log out and log back in, or source your .bashrc
   source ~/.bashrc
   nvm install --lts
   nvm use --lts
   sudo npm install pm2 -g
   ```
6. This agent will now appear in your pool, ready to execute deployment jobs.
7. 
