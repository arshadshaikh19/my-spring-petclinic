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
                            withSonarQubeEnv('Sonarqube 9.9.3') {
                                    sh script: 'mvn clean package -Dcheckstyle.skip'
                                    sh script: 'mvn clean verify sonar:sonar -Dcheckstyle.skip \
                                        -Dsonar.projectKey=demoapp-project \
                                        -Dsonar.host.url=http://34.131.248.172:9000 \
                                        -Dsonar.login=sqp_5879d760de6fe80ed916340a027c715f2f2b3dba'
                        }
                        }
                }
                 stage('Artifact'){
                        steps{
                                dir('/home/my/workspace/Springpet/target')
                                nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: 'spring-petclinic-3.1.0-SNAPSHOT.jar', type: 'jar']], credentialsId: 'admin', groupId: 'org.springframework.samples', nexusUrl: '34.131.248.172:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'testrepositories', version: '3.1.0-SNAPSHOT'
                        }
                }
        }
}
