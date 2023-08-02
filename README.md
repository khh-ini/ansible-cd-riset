# ansible-cd-riset

![Screenshot from 2022-06-26 22-37-13](https://github.com/khhini/riset-ansibel-cd/assets/50735459/961f1a50-d831-4d85-9d5a-e2fa5c8e5b97)

An illustrative project aimed at exploring the capabilities of Ansible as a Continuous Delivery tool through a Zero Downtime Rolling Update scenario.

This project leverages the following components:
- GitHub
- Ansible
- DockerHub
- Google Compute Engine
- Jenkins
- HAProxy

In this project setup, GitHub serves as the source code repository, enabling developers to push their code and thereby trigger the CI/CD pipeline. Jenkins assumes the role of providing the CI pipeline, which automatically initiates whenever a developer pushes a new commit to the repository. Within the CI pipeline, various testing and building steps are executed, culminating in the pushing of the application to DockerHub.

Once the CI pipeline successfully completes its tasks, Jenkins proceeds to trigger the CD pipeline. This CD pipeline is responsible for executing an Ansible playbook, orchestrating the deployment of the application through the Rolling Update deployment approach. This method ensures a gradual update of servers, performed sequentially.

During the Ansible-driven deployment, crucial steps are taken. Ansible dynamically reconfigures HAProxy, which serves as the traffic manager, overseeing the distribution of incoming requests to the servers. Initially, one server is strategically removed from the load balancing pool to enable its deployment with the new version of the application.

Upon the successful deployment of the new version on the chosen server, Ansible conducts a comprehensive health check to verify the application's capacity to handle incoming traffic. If the health check yields positive results, Ansible reconfigures HAProxy once again. This time, the newly updated server is reintegrated into the server pool, while another server is temporarily removed. This cyclical process continues, ensuring a controlled and smooth deployment process for the updated application.
