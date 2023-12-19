pipeline {
    agent any

    stages {
        stage('Checkout') {
                    steps {
                        git branch: env.BRANCH_NAME ,url: env.GIT_URL, credentialsId: 'github-pat'
                    }
                }
        stage('get merge commit'){
            steps {
                script{
                if(env.BRANCH_NAME.matches('feature.*')){
                    sh 
                    """
                    git checkout develop
                    git checkout ${env.BRANCH_NAME}
                    """
                    def merge_commit = sh(script: "git merge-base ${env.BRANCH_NAME} develop", returnStdout: true)
                    echo "this is merge commit : ${merge-commit}"
                    sh(script: "git diff ${merge-commit} HEAD --name-only > changedfiles.txt", returnStdout: true)
                    sh 
                    """ 
                    ls -lrt
                    cat changedfiles.txt
                    """

                }
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
