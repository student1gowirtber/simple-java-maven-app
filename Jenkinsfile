pipeline {
    agent any
    parameters {
        string(
            name: 'BRANCH_NAME',
            defaultValue: 'main',
            description: 'Branch Name'
            )}
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Wait') {
            steps {
                script { 
                def timeoutDuration = (BRANCH_NAME == 'main') ? 30 : 15
                timeout(time: timeoutDuration, unit: 'MINUTES') { 
                    echo 'Build läuft ...' + BRANCH_NAME + 'branch .... '} 
            }
        } }
        stage('Test') { 
            steps {
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
    }
}
