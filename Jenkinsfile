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
                                sh script: 'mvn package'
                        }
                }
                stage('Code Analysis'){
                        steps{
                            withSonarQubeEnv(credentialsId: 'sonarqube-user-token', installationName: 'Sonarqube-9.9.3') {
                                // some block
                                mvn clean verify sonar:sonar \
                                    -Dsonar.projectKey=springpet-clinic \
                                    -Dsonar.host.url=http://34.131.143.64:9000 \
                                    -Dsonar.login=sqp_e2f726f25b10f826720a0f46fd50d7bfab612e31
                            }
                        }
                }
        }
}
