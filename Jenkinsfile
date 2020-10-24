pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          steps {
              git 'https://github.com/pranikita/maven-project-1.git'
            }
        }
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

        stage ('build && SonarQube analysis') {
            steps {
		withSonarQubeEnv('Sonar_Server') {
                    withMaven(maven : 'LocalMaven') {
                        sh 'mvn clean package sonar:sonar'
                    }
		}	
            }
        }
}
}
