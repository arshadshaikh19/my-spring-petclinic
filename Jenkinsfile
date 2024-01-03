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
                                sh script: 'mvn clean package'
                        }
                }
                stage('SonarQube analysis') {

                        steps{
                                withSonarQubeEnv('sonarqube-10.0') {
                                        sh "mvn sonar:sonar\
                                          -Dsonar.projectKey=demoapp-project \
                                          -Dsonar.projectName='demoapp-project' \
                                          -Dsonar.host.url=http://34.131.248.172:9000 \
                                          -Dsonar.token=sqp_97c01e9da80440e27adf154756941d88744a9455"
                                }
                        }
                }
        }
}
