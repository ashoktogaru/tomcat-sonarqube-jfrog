pipeline {
    agent any
    stages {
        stage('Stage-0 : Static Code Analysis Using SonarQube') { 
            steps {
               sh 'mvn clean verify sonar:sonar'
            }
        }
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ashoktogaru/tomcat-sonarqube-jfrog.git']]])
            }
        }        
        stage('Clean') {
            steps {
               sh ('mvn clean');
            }
        }
        
        stage('Validate') {
            steps {
                sh ('mvn validate');
            }
        }
        
        stage('Compile') {
            steps {
                sh ('mvn compile');
            }
        }
        
        stage('Test') {
            steps {
                sh ('mvn test');
            }
        }
        
        stage('Package') {
            steps {
                sh ('mvn package');
            }
        }
        
        stage('Verify') {
            steps {
                sh ('mvn verify');
            }
        }
        
        stage('Install') {
            steps {
                sh ('mvn install');
            }
        }
             stage('Stage-8 : Deploy an Artifact to Artifactory Manager i.e. Nexus/Jfrog') { 
            steps {
                sh 'mvn deploy -DskipTests'
            }
        }

            
         stage('Stage-9 : Deployment - Deploy a Artifact devops-3.0.0-SNAPSHOT.war file to Tomcat Server') { 
            steps {
                sh 'curl -u admin:redhat@123 -T target/**.war "http://35.154.13.203:8080/manager/text/deploy?path=/ashok&update=true"'
            }
        } 
  
          stage('Stage-10 : SmokeTest') { 
            steps {
                sh 'curl --retry-delay 10 --retry 5 "http://35.154.13.203:8080/ashok"'
            }
       }
        }
          
    }

