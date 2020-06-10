node{
   stage('SCM Checkout'){
     git 'https://github.com/YashasviNerali/sample-web-application-1'
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
   withCredentials([string(credentialsId: 'docker-password', variable: 'dockerHubPwd')]) {
   sh "docker login -u yashasvinerali -p ${dockerHubPwd}"
}
  
   sh 'docker push yashasvinerali/my-app:1'
   


     
