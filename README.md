# CI / CD pipeline infrastructure for a liferay module
This repo builds a CI / CD pipeline infrastructure including the following components:
* [LIFERAY Server](https://hub.docker.com/r/liferay/liferay-portal/) 
* [Jenkins Build Server](https://hub.docker.com/r/tribunex/jenkins-maven/)
* [Nexus Repository Manager](https://hub.docker.com/r/sonatype/nexus3/)

## Configuration
The following configuration of components is required to make things work:

### Jenkins
The credentials for the NEXUS repository need to be configured as Jenkins global credentials. Create the following credentials of type text:
* 'NEXUS_USERNAME'
* 'NEXUS_PASSWORD'

### NEXUS 
The maven-release repository should allow to redeploy a component. Therefore, set the corresponding *Deployment Policy* to *Allow redeploy* (see [NEXUS documentation](https://help.sonatype.com/repomanager3/configuration/repository-management#RepositoryManagement-ManagingRepositoriesandRepositoryGroups))

## Local development
Pushing local builds to the Nexus server is possible by setting the Nexus hostname in the environmental varibale `NEXUS_HOSTNAME`. The variables for Jenkins must also be specified. 

Use the settings.xml for your maven build commands:
    
    mvn --settings.xml path_to_this_repo/jenkins/settings.xml install


## Run this pipeline infrastructure

    docker-compose up -d

## State 
NEXUS and Jenkins container store their state at `path_to_this_repo/container_storage`.