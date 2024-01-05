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
                                sh script: 'mvn clean package -Dcheckstyle.skip'
                                sh script: 'mvn clean verify sonar:sonar -Dcheckstyle.skip \
  -Dsonar.projectKey=springpet-clinic \
  -Dsonar.host.url=http://34.131.45.90:9000 \
  -Dsonar.login=sqp_506c455d39efa17039f66759bedab75cd19ed6ef'    
                            }
                        }
                }
        }
}
