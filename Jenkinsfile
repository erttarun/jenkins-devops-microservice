pipeline {
		 agent any
                //agent { docker { image 'maven:3.6.3'} }
                environment {
                    dockerHome = tool 'myDocker'
                    mavenHome = tool 'myMaven'
                    PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
                }
                stages {
                   stage('Checkout') {
                       steps {
                          sh 'mvn --version'
                          sh 'docker --version'
                          echo "Build"
                          echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                          echo "BUILD_ID - $env.BUILD_ID"
                       }
                   }
                   stage('Compile') {
                       steps {
                          sh "mvn clean compile"
                          echo "Build"
                       }
                   }
                   stage('Test') {
                       steps {
                          sh "mvn test"
                       }
                   }
                   stage('Integration Test') {
                       steps {
                          sh "mvn failsafe:integration-test failsafe:verify"
                       }
                   }
                   stage('Package') {
                       steps {
                          sh "mvn package -DskipTests"
                       }
                   }
                   stage('Build docker image') {
                       steps {
                          // docker build -t in18min/currency-exchange-devops:$env.BUILD_TAG
                          script {
                            dockerImage=docker.build("in18min/currency-exchange-devops:$env.BUILD_TAG")                          

                          }
                       }
                   }
                   stage('Push docker image') {
                       steps {
                          script {
                        docker.withRegistry('','dockerhub') {
                        dockerImage.push();
                       dockerImage.push('latest');
}
                               
}
                       }
                   }
           }
}
