node {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git credentialsId: '2b42f2c3-d551-4ee8-9636-c8f0c47ad24c', url: 'https://github.com/rakeshlodhigit/MVCProject.git'

               
                // To run Maven on a Windows agent, use
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    
                    archiveArtifacts 'target/*.war'
                    
                    
                    
                    
                }
                
            }
        }
        stage('deploy'){
            steps{
                deploy adapters: [tomcat7(credentialsId: '614c7d58-ecdd-4240-a5d5-dc64167a42cf', path: '', url: 'http://localhost:8081')], contextPath: 'mvcwebapp', war: '**/*.war'
            }
        }
    }
}
