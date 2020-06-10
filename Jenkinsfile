node{
   stage('SCM Checkout'){
     git 'https://github.com/YashasviNerali/devopscicd'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven', type: 'maven'
        withSonarQubeEnv('sonar') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
    
    stage ('Build Docker Image') {
     sh 'docker build -t yashasvinerali/my-app:1 .'
   }
   
   stage('Push Docker image'){
   withCredentials([string(credentialsId: 'docker_password', variable: 'docker_password')]) {
   sh "docker login -u yashasvinerali -p ${docker_password}"
}
  
   sh 'docker push yashasvinerali/my-app:1'
   
   
   
   }
   
   }


     
