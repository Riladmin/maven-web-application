node
{

 def mavenHome = tool name: "maven3.8.4"

 stage('CheckoutCode')
 {
 git branch: 'development', credentialsId: 'e782fdc4-245b-432e-b9d5-c59484c70b54', url: 'https://github.com/Riladmin/maven-web-application.git'
 }

 stage('Build'){
 sh "${mavenHome}/bin/mvn clean package"
 }

 stage('ExecuteSonarQubeReport'){
 sh "${mavenHome}/bin/mvn clean sonar:sonar"
 }

 stage('UploadArtifactIntoNexus'){
 sh "${mavenHome}/bin/mvn clean deploy"
 }

 stage('DeployAppintoTomcat'){
 sshagent(['620e46b5-5c5a-41f5-83e2-58e6f6326499']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.91.17:/opt/apache-tomcat-9.0.60/webapps"
 }

 }
 
 stage('sendNotifications'){
 emailext body: '''Build over

''', subject: 'Build over', to: 'enthotibalaji2014@gmail.com'

 }

 }
