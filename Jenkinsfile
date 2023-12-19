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
                // if(env.BRANCH_NAME.matches('feature.*')){

                //     sh(script: "git checkout  remotes/origin/develop", returnStdout: true).trim()
                //     sh(script: "git checkout  ${env.BRANCH_NAME}", returnStdout: true).trim()
                //     def merge_commit = sh(script: "git merge-base remotes/origin/${env.BRANCH_NAME} remotes/origin/develop", returnStdout: true).trim()
                //     echo "this is merge commit : ${merge_commit}"
                //     sh(script: "git diff ${merge_commit} HEAD --name-only > changedfiles.txt")
                //     sh(script: "git status")
                //     sh(script: "pwd")
                //     sh(script: "ls -lrt")
                //     sh(script: "cat changedfiles.txt")
                // }

                if (currentBuild.number == 1) {
                        // Define the tag name based on branch name
                        def tagName = "marge-base-${env.BRANCH_NAME}"


                        withCredentials([usernamePassword(credentialsId: 'githubcred', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                            sh """
                                git config user.name ${GIT_USER}
                                git config user.email saishivam538@outlook.com
                                git tag ${tagName}
                                git push https://${GIT_USER}:${GIT_PASS}@${env.GIT_URL} ${tagName}
                            """
                        }
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
