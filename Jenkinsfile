pipeline {
    agent any
    environment {
        CSRF_TOKEN = credentials('Jenkins_Secret_Text_Token')
    }
    stages {
        stage('Create Secret') {
            steps {
                sh "sed -e 's,{{SECRET_KEY}},'${CSRF_TOKEN}',g;' credentials.yaml | kubectl apply -f -"
            }
        }
        stage('Deploy App') {
            steps {
                sh "kubectl apply -f todo.yaml"
                sh "sleep 50"
                sh "kubectl get svc todo"
            }
        }
    }
}