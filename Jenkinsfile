@Library('pipeline-library-demo')_
node('maven-label') {
   def mvnHome
   
   stage('sharedlib demo'){
    sayHello "Jenkins"
   }
   stage('Preparation') { // for display purposes
      
      git 'https://github.com/shopping-cart-app/shopping-cart.git'
              
      mvnHome = tool 'maven'
   }
   stage('Build') {
      
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
