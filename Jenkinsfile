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
                          sh "mv test"
                       }
                   }
                   stage('Integration Test') {
                       steps {
                          sh "mvn failsafe:integration-test failsafe:verify"
                       }
                   }
           }
}
