How server was created

Terrafrom will then

    docker pull ugbechie/jenkins-server:0.1
    docker run -d --name jenkins-server -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock -v $JENKINS_HOME:/var/jenkins_home  ugbechie/jenkins-server:0.1



Add Following plugins

Pipeline: Supporting APIs /
Pipeline job /
Pipeline: Nodes and Processes /
Pipeline: Groovy /
Pipeline: Basic Steps /
Pipeline: Stage Step /
Pipeline: Multibranch /
Pipeline: Input Step /
Pipeline: Build Step /
Pipeline: Shared Groovy Libraries /
Pipeline Graph Analysis /
Pipeline: Milestone Step /
Pipeline: Stage Tags Metadata /
Pipeline: Model API /
Pipeline: REST API /
Pipeline: Stage View /
Pipeline: Declarative Extension Points API /
Pipeline: Declarative /
Pipeline /
GitHub Branch Source /
Docker Pipeline /
Pipeline: Declarative Agent API /
Pipeline: GitHub Groovy Libraries /



Add following othe plugins 

SSH Agent plugin  /  

        This plugin prgress the credentials id created by Jenkins ssh key config into workspaces created where scripts run
        
Workspace Cleanup pluging

        Enables cleaning up of woprkspaces in Jenkinsfile
        

Add gitlab priovate key

        cd ~/.ssh
        cat id_rsa
        goto
             Manage Jenkins
             ManageCredentials
             Jenkins
                Add credentials
                    Drop down boix : SSH wiith username
                    id : gitlab
                    username : jenkins
                        Add
                            paste private key
                        Okay
                        
Add Docker registry credentials

        cd ~/.ssh
        cat id_rsa
        goto
             Manage Jenkins
             ManageCredentials
             Go to Jenkins 
               click global [ drop down]
                 Add credentials
                    Drop down boix : password wiith username
                    id : registry
                    username : admin 
                    password : admin@1969
                save        
                                                

Create pipeline

        New Item
            select pipeline
            
        Under pipline
            select from scm
            sel;ect git from dropdown
            put URL of jenkins gitlab :    git@gitlab.platform-engineering.com:opportunities/container-pipeline/jenkins.git
            select jenkins [username set up above ]
            
        Apply
        Save
        
        This will auto,atically pick up Jenkinsfile
        
        
Running

Uses Sample Project : branch tester-jenkins
Uses brass-hands  : branch jenkins-pipeline


Some changes in pipeline

   1. Correct to decision over jq or unix in pasckagecheck.sh forund in components of brass-hands
   
   2. Had to remove colon from file : trivy.sh  
     docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
    -v $HOME/Library/Caches aquasec/trivy sample-app:0.0.1 > sample-app:0.0.2-trivy-results.txt\

   3. chnage to pipeline.sh to ref tester-jenkins of Sample Project
   
   4. Update ro registry.sh  to use Docker registry built for Pipeline project : registry.mydocker.ga  [ switch added ]
   

