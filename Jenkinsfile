pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/afrinpinjari/maven-project.git'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'localMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'localMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'localMaven') {
                    sh 'mvn install'
                }
            }
        }

         stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcat1']) {
                 sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@172.31.20.132:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
