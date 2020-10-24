pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git branch: 'ci-cd-pipeine-1', url: 'https://github.com/pranikita/maven-project-1.git'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'local_mvn_v3.5_p1') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'local_mvn_v3.5_p1') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'local_mvn_v3.5_p1') {
                    sh 'mvn install'
                }
            }
        }

        stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcat_dev_server']) {
                 sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@172.31.80.143:/var/lib/tomcat/webapps'
      } 
}
}
    }
}
