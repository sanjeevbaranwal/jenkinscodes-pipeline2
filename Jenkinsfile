// see https://dzone.com/refcardz/continuous-delivery-with-jenkins-workflow for tutorial
// see https://documentation.cloudbees.com/docs/cookbook/_pipeline_dsl_keywords.html for dsl reference
// This Jenkinsfile should simulate a minimal Jenkins pipeline and can serve as a starting point.
// NOTE: sleep commands are solelely inserted for the purpose of simulating long running tasks when you run the pipeline
node {
   // Mark the code checkout 'stage'....
     stage 'checkout'

   // Get some code from a GitHub repository
   git url: 'https://github.com/sanjeevbaranwal/JenkinsCodes-pipeline.git'
   sh 'git clean -fdx; sleep 4;'

   // Get the maven tool.
   // ** NOTE: This 'mvn' maven tool must be configured
   // **       in the global configuration.
   def mvnHome = tool 'mvn'

   stage 'build'
   // set the version of the build artifact to the Jenkins BUILD_NUMBER so you can
   // map artifacts to Jenkins builds
   sh "${mvnHome}/bin/mvn versions:set -DnewVersion=$bname.${env.BUILD_NUMBER}.${env.BUILD_TIMESTAMP}"
   //sh "${mvnHome}/bin/mvn versions:set -DnewVersion=${env.BUILD_NUMBER}"
   sh "${mvnHome}/bin/mvn package"

   stage 'test'
   parallel 'test': {
     //sh "${mvnHome}/bin/mvn test; sleep 2;"
   }, 'verify': {
     //sh "${mvnHome}/bin/mvn verify; sleep 3"
   }

   stage 'archive'
   //archive 'target/*.jar'
}


node {
   stage 'deploy Canary'
   sh 'echo "write your deploy code here"; sleep 5;'
   sh '(sshpass -p "tomcat" scp README.md tomcat@18.220.169.91:/tmp)'
   
   stage 'ansible'
   sh 'ansible --version'

   stage 'deploy Production'
   input 'Proceed?'
   //sh 'echo "write your deploy code here"; sleep 6;'
   //archive 'target/*.jar'
}
