pipeline {
    agent any
    environment {
          APP_NAME = "redditcaching"
    }
    stages {
         stage("Cleanup Workspace") {
             steps {
                cleanWs()
             }
         }
         stage("Checkout from SCM") {
             steps {
                     git branch: 'main', credentialsId: 'GithubCredentialToken', url: 'https://github.com/MOUSSASeddik/GitOpsProject.git'
             }
         }
         stage("Update the Deployment Tags") {
            steps {
                sh """
                    cat deployment.yaml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }
         }
         stage("Push the changed deployment file to GitHub") {
            steps {
                sh """
                    git config --global user.name "MOUSSASeddik"
                    git config --global user.email "medseddikmoussa@gmail.com"
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'GithubCredentialToken', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh """
                        git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/MOUSSASeddik/GitOpsProject.git main
                    """
                }
            }
        }

    }
}
