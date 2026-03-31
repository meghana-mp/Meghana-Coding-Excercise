pipeline {
    agent any

    stages {
        stage('Parallel execution') {
            parallel {
                // 1. Java/Maven Stage
                stage('Java') {
                    steps { sh 'mvn clean test' }
                }

                // 2. Python Stage
                stage('Python') {
                    steps {
                        sh '''
                            python3 -m venv venv
                            . venv/bin/activate
                            pip install -r requirements.txt
                            pytest
                        '''
                    }
                }

                // 3. JS & TS Stage (Playwright)
                stage('Playwright') {
                    steps {
                        sh '''
                            npm install
                            npx playwright install --with-deps
                            npx playwright test
                        '''
                    }
                }
            }
        }
    }
}