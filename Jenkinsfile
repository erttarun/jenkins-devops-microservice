pipeline {
		 agent any
                //agent { docker { image 'maven:3.6.3'} }
                stages {
                   stage('Build') {
                       steps {
                         //sh 'mvn --version'
                          echo "Build"
                          echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                          echo "BUILD_ID" - $env.BUILD_ID"
                       }
                   }
                   stage('Test') {
                       steps {
                          echo "Test"
                       }
                   }
                   stage('Integration Test') {
                       steps {
                          echo "Integration Test"
                       }
                   }
           }
}
