This repository consists of Azure vm installation,terraform code to create server on aws , jenkins installation ,java installation and jenkins groovy script to deploy K8s

#install_jenkins.yml

Installs Jenkins CI on RHEL/CentOS and Debian/Ubuntu servers.

Requirements
Requires curl to be installed on the server. Also, newer versions of Jenkins require Java 8+ (see the test playbooks inside the molecule/default directory for an example of how to use newer versions of Java for your OS).

#install_java.yml
Installs Java for RedHat/CentOS and Debian/Ubuntu linux servers.

The defaults provided by this role are specific to each distribution.
java_packages:
  - java-1.8.0-openjdk


#azurevm.yml
installs vm on azure and does the configuration
installs dependencies
creates subnets 
creates resourcegroup
creates virtualnetwork
created publicip
creates security group
create vm


#jenkinsgroovy 
creates and deploys k8s and deploys java app hello-java
podTemplate(label: 'jenkins-pipeline', containers: [
    containerTemplate(name: 'jnlp', image: 'jenkinsci/jnlp-slave:2.62', args: '${computer.jnlpmac} ${computer.name}', workingDir: '/home/jenkins', resourceRequestCpu: '500m', resourceLimitCpu: '500m', resourceRequestMemory: '1024Mi', resourceLimitMemory: '1024Mi'),
    containerTemplate(name: 'docker', image: 'docker:1.12.6', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'maven', image: 'maven:3.5.0-jdk-8', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'helm', image: 'lachlanevenson/k8s-helm:v2.6.1', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.3', command: 'cat', ttyEnabled: true)

