pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/pranikita/maven-project-1'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                }
            }
        }

        stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcat']) {
                 sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@3.84.11.17:/var/lib/tomcat/webapps'
      } 
}
}
    }
}
