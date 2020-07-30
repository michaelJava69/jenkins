pipeline {
    agent any

    environment {
       USER = "michaelugbechie"
    }
    
      
    stages {

       
       stage('Clean Workspace') {
           steps {
               // Clean the workspace
               sh 'echo "clean workspace"'
               cleanWs()

           }
       }



       stage('Clone ReportService') {
        steps {


            sh 'mkdir -p Assurance/Source_Code_Repo/report_service'


            dir("Assurance/Source_Code_Repo/report_service")
            {
                git branch: "master",
                credentialsId: 'gitlab',
                url: 'git@gitlab.platform-engineering.com:opportunities/container-pipeline/assurance/source_code_repo/report_service.git'
            }
         }
       }

       stage('Clone Registry') {
        steps {
            
            
            sh 'mkdir -p Assurance/Source_Code_Repo/registry'             
            

            dir("Assurance/Source_Code_Repo/registry")
            {
                git branch: "master",
                credentialsId: 'gitlab',
                url: 'git@gitlab.platform-engineering.com:opportunities/container-pipeline/assurance/source_code_repo/registry.git'
            }
         }
       }


       stage('Clone CommonFunctions') {
        steps {


            sh 'mkdir -p Functionality/Source_Code_Repo/common-functions'


            dir("Functionality/Source_Code_Repo/common-functions")
            {
                git branch: "master",
                credentialsId: 'gitlab',
                url: 'git@gitlab.platform-engineering.com:opportunities/container-pipeline/functionality/source-code-repo/common-functions.git'
            }
         }
       }
       
    
       stage('Clone BrassHand and run pipeline') {
        steps {
            sh 'mkdir -p brass-hand'
            dir("brass-hand")
            {
                git branch: "jenkins-pipeline",
                credentialsId: 'gitlab',
                url: 'git@gitlab.platform-engineering.com:opportunities/container-pipeline/brass-hand.git'
                withDockerRegistry([credentialsId: 'registry', url: "http://registry.mydocker.ga"]) {
                   sshagent(credentials: ['gitlab']) {
                      script {
                         try {
                            sh './run_pipeline.sh'
                         } catch (Exception e) {
                             echo ' - Jenkins Build Broken '
                             currentBuild.result = ' FAILURE '
                         }
                      }
                   
                      // sh './run_pipeline.sh'
                      sh 'echo $pwd " is workspace"'
                   }  
                }
            }
         }
       }

    }
}

