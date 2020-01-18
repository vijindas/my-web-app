pipeline{
  agent any
  tools {
      git 'git'
      maven 'maven'
}

  environment {
        IMAGE_TAG = "${env.BUILD_NUMBER}"

  }

stages{

   stage('SCM Checkout'){
     steps{
      git 'https://github.com/vijindas/my-web-app.git'
     }
   }

   stage('Unit Testing'){
     steps{
             bat label: '', script: 'mvn clean test'
     }
   }
      stage('Maven packing'){
     steps{
           bat label: '', script: 'mvn clean package'
        }
    }

   stage('Input') {
            steps {
                input('Do you want to proceed to dev?')
            }

    }

   stage('Maven Deploy'){
     steps{
    deploy adapters: [tomcat8(credentialsId: 'a1839dca-78d9-488b-877f-1e385269a87a', path: '', url: 'http://PC:8089/')], contextPath: '/simple-web-app', onFailure: false, war: '**/*.war'
       }
    }
   
}
}