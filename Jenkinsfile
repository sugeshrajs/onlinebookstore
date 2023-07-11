pipeline {
agent any
    stages {
        stage('SCM') {
            steps {
                // Get some code from a GitHub repository
                git credentialsId: 'github_credentials', url: 'https://github.com/sugeshrajs/onlinebookstore.git'
                }
        }
        stage('Build') {
            steps {
                // maven packages
                    sh "mvn -Dmaven.test.failure.ignore=true clean package" 
                }
       }
       stage('Artifacts') {
            steps {
                    archiveArtifacts 'target/*.war' 
                }
       }
       stage('Deploy') {
            steps {
                    sh "curl -v -u admin:admin -T /var/lib/jenkins/workspace/bookstore/target/onlinebookstore.war 'http://52.66.253.161:8080/manager/text/deploy?path=/bookstore&update=true'"
                }
       }
       
    }
}
