# Azure DevOps Self-Hosted Agent Setup
Steps to install a small agent on your VM (the CI/CD server) that listens for jobs from your Azure DevOps pipeline.

1. In your Azure DevOps project, go to Project Settings > Agent Pools.
2. Create a new pool (e.g., "My-Lab-VMs").
3. On your Linux VM, follow Microsoft's guide to install and configure the self-hosted agent. This involves downloading a script and running it.
4. This agent will now appear in your pool, ready to execute deployment jobs.
