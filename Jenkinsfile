pipeline {
    agent any
    stages {        
        stage('Build Application') {
            steps {
                sh '/opt/maven/bin/mvn -f pom.xml clean install package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Deploy Application') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat_user', path: '', url: 'http://34.205.33.125:8080')], contextPath: 'webapp', war: '**/*.war'
            }            
        }       

    }
}
