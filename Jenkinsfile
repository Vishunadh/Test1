Skip to content
Search or jump to…
Pull requests
Issues
Marketplace
Explore
 
@Vishunadh 
vamsijakkula
/
hellowhale
Public
forked from janakiramm/hellowhale
1
1272
Code
Pull requests
1
Actions
Projects
Wiki
Security
Insights
hellowhale/Jenkinsfile
@vamsijakkula
vamsijakkula Create Jenkinsfile
Latest commit ce0a614 on Jun 2, 2020
 History
 1 contributor
43 lines (34 sloc)  901 Bytes
  
pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/vamsijakkula/hellowhale.git', branch:'master'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("vamsijakkula/hellowhale:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
© 2021 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
