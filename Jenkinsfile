
        stage("Push the changed deployment file to GitHub") {
           steps {
                sh """
                    git config --global user.name "MOUSSASeddik"
                    git config --global user.email "medseddikmoussa@gmail.com"
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'sshGithubJenkServerGUI', gitToolName: 'Default')]) {
                    sh "git push https://github.com/MOUSSASeddik/GitOpsProject.git main"
                }
            }

        }
