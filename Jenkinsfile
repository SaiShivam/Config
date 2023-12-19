pipeline {
    agent any

    stages {
        stage('Checkout') {
                    steps {
                        git branch: env.BRANCH_NAME ,url: env.GIT_URL
                    }
                }
        stage('get merge commit'){
            steps {
                if(env.BRANCH_NAME.matches('feature*')){

                    def merge-commit = sh(script: "git merge-base ${env.BRANCH_NAME} develop", returnStdout: true)
                    echo "this is merge commit : ${merge-commit}"
                    sh(script: "git diff ${merge-commit} HEAD --name-only > changedfiles.txt", returnStdout: true)
                    sh 
                    """ 
                    cat changedfiles.txt
                    """

                }
                
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
