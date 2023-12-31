def mergeBaseCommit = ""
pipeline {
    agent any

    stages {
        stage('Checkout') {
                    steps {
                        git branch: env.BRANCH_NAME ,url: env.GIT_URL, credentialsId: 'githubcred'
                    }
                }
        stage('create merge-base commit'){
            steps {
                script{


                if (currentBuild.number == 1) {
                        // Define the tag name based on branch name
                        def tagName = "merge-base-${env.BRANCH_NAME}"
                        def repoURL = env.GIT_URL.replaceAll(/^https?:\/\//, '') // Remove the 'http://' or 'https://' part of the URL

                        withCredentials([usernamePassword(credentialsId: 'githubcred', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                            def tagExistsLocally = sh(script: "git tag | grep -w ${tagName}", returnStatus: true) == 0
                            def tagExistsRemotely = sh(script: "git ls-remote --tags origin | grep -w refs/tags/${tagName}", returnStatus: true) == 0
                            echo "tagExistsLocally: ${tagExistsLocally}"
                            echo "tagExistsRemotely: ${tagExistsRemotely}"
                            if (tagExistsLocally == false && tagExistsRemotely == false) {
                            sh """
                                git tag -d ${tagName} || true
                                git config user.name ${GIT_USER}
                                git config user.email saishivam538@outlook.com
                                git tag ${tagName}
                                git push https://${GIT_USER}:${GIT_PASS}@${repoURL} ${tagName}
                            """
                            }


                        }
                    }
                }
                
            }
        }


        stage('fetch merge-base commit'){
            steps{

                script{
                     if(!env.BRANCH_NAME.matches('develop.*')){

                        mergeBaseCommit = sh(script: "git rev-list -n 1 merge-base-${env.BRANCH_NAME}", returnStdout: true).trim()
                        echo "Merge Base Commit for ${env.BRANCH_NAME} is ${mergeBaseCommit}"
                     }
                }
            }
        }

        stage('get changed files'){
            steps{
                script{

                    if(!env.BRANCH_NAME.matches('develop.*')){

                        sh(script: "git checkout  remotes/origin/develop", returnStdout: true).trim()
                        sh(script: "git checkout  ${env.BRANCH_NAME}", returnStdout: true).trim()
                        // def merge_commit = sh(script: "git merge-base remotes/origin/${env.BRANCH_NAME} remotes/origin/develop", returnStdout: true).trim()
                        // echo "this is merge commit : ${merge_commit}"
                        sh(script: "git diff ${mergeBaseCommit} HEAD --name-only > changedfiles.txt")
                        sh(script: "git status")
                        sh(script: "pwd")
                        sh(script: "ls -lrt")
                        sh(script: "cat changedfiles.txt")
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
