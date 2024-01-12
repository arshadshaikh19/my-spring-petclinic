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
                                sh script: 'mvn package \
                                -Dcheckstyle.skip'
                        }
                }
                 stage('Code Analysis'){
                        steps{
                            withSonarQubeEnv(credentialsId: 'sonarqube-user-token', installationName: 'Sonarqube-9.9.3') {
                                // some block
                                sh script: 'mvn clean verify sonar:sonar \
                                    -Dcheckstyle.skip \
                                    -Dsonar.projectKey=springpet-clinic \
                                    -Dsonar.host.url=http://34.131.143.64:9000 \
                                    -Dsonar.login=sqp_e2f726f25b10f826720a0f46fd50d7bfab612e31'
                            }
                        }
                }
                 stage('Artifact'){
                        steps{
                                dir('/home/my/workspace/Springpet/target'){
                                        nexusArtifactUploader artifacts: [[artifactId: 'spring-boot-starter-parent', classifier: '', file: 'spring-petclinic-3.1.0-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'org.springframework.boot', nexusUrl: '34.131.45.90:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'testrepo', version: '3.1.0-SNAPSHOT'
                                }
                        }
                }
        
        }
}
