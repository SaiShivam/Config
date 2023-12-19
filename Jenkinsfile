pipeline {
    agent any

    stages {
        stage('Checkout') {
                    steps {
                        git branch: env.BRANCH_NAME ,url: env.GIT_URL, credentialsId: 'githubcred'
                    }
                }
        stage('get merge commit'){
            steps {
                script{
                if(env.BRANCH_NAME.matches('feature.*')){

                    sh(script: "git checkout  remotes/origin/develop", returnStdout: true).trim()
                    sh(script: "git checkout  ${env.BRANCH_NAME}", returnStdout: true).trim()
                    def merge_commit = sh(script: "git merge-base remotes/origin/${env.BRANCH_NAME} remotes/origin/develop", returnStdout: true).trim()
                    echo "this is merge commit : ${merge_commit}"
                    sh(script: "git diff ${merge_commit} HEAD --name-only > changedfiles.txt")
                    sh(script: "pwd", returnStdout: true)
                    sh(script: "ls -lrt", returnStdout: true)
                    sh(script: "cat changedfiles.txt", returnStdout: true)
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
