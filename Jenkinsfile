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
                withMaven(maven : 'local_maven_3') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'local_maven_3') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'local_maven_3') {
                    sh 'mvn install'
                }
            }
        }

        stage ('deploy to tomcat') {
             steps {
                 sshagent(['app']) {
                 sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@3.90.107.21:/var/lib/tomcat/webapps'
      } 
}
}
    }
}
