pipeline {
    agent any
    environment {
        GIT_CREDENTIALS = credentials('github-credentials') // Add the ID of your GitHub credentials
    }
    stages {
        stage('Clone Repository') {
            steps {
                // Use GitHub credentials to clone the repository
                git branch: 'master', 
                    url: 'https://github.com/EyesOnCloud/git-jenkins-integration.git',
                    credentialsId: 'github-credentials'
            }
        }
        stage('Set Up Python Environment') {
            steps {
                script {
                    sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    '''
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'pip install -r requirements.txt || echo "No requirements file"'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    sh 'python3 -m unittest discover'
                    // Execute test_main.py to see custom test output in the console
                    sh 'python3 test_main.py'
                }
            }
        }
    }
    post {
        always {
            echo 'Build finished'
        }
        success {
            echo 'Build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
