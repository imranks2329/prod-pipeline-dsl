    pipeline {
        agent any
        stages {
            stage('Build Application') {
                steps {
                    sh 'mvn -f pom.xml clean package'
                }
                post {
                    success {
                        echo "Now Archiving the Artifacts...."
                        archiveArtifacts artifacts: '**/webappcook.war'
                    }
                }
            }
            stage('Deploy in Staging Environment'){
                steps{
                    build job: 'pipeline-tomcat-test-dsl'
     
                }
                
            }
            stage('Deploy to Production'){
                steps{
                    timeout(time:5, unit:'DAYS'){
                        input message:'Approve PRODUCTION Deployment?'
                    }
                    build job: 'pipeline-tomcat-pro-dsl'
                }
            }
        }
    }
