pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Create Test Code') {
            steps {
                // SonarQube needs at least one source file to analyze
                sh '''
                    mkdir -p src
                    cat > src/hello.js <<'EOF'
function add(a, b) {
  return a + b;
}
console.log(add(2, 3));
EOF
                '''
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                        ${scannerHome}/bin/sonar-scanner \
                          -Dsonar.projectKey=sonara-a \
                          -Dsonar.projectName='sonara-a' \
                         
                    '''
                }
            }
        }
    }
}
