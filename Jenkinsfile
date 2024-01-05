pipeline{

        agent { label 'worker' }

         stages{
                stage('Source code'){
                        steps{
                                git url: 'https://github.com/arshadshaikh19/my-spring-petclinic.git', branch: 'main'
                        }
                }
                stage('Build code'){
                        steps{
                            withSonarQubeEnv('Sonarqube 9.9.3'){
                                sh script: 'mvn clean package sonar:sonar'
                            }
                        }
                }
        }
}
