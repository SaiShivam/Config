pipeline {
    agent any

    stages {
        stage('Checkout') {
                    steps {
                        git branch: env.BRANCH_NAME ,url: env.GIT_URL
                    }
                }

        // Add other stages as needed
        stage('Build') {
            steps {
                // Your build steps go here
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                // Your testing steps go here
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            steps {
                // Your deployment steps go here
                echo 'Deploying...'
            }
        }
    }
}
