node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'sameh-github-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        //sh "git remote set-url origin https://${USER}:${PASS}@github.com/samehpalas/argo-cd.git"
                        sh "git remote set-url origin https://${USER}:${PASS}@github.com/samehpalas/argo-cd.git"
                        sh 'git config --global user.email "samehpalas33@gmail.com"'
                        sh 'git config --global user.name "samehpalas"'
                        sh "git remote -v"
                        sh "git log --oneline"
                        //sh "git switch main"
                        sh "cat app/deployment.yaml"
                        sh "sh artifact_version_update app/deployment.yaml"
                        sh "echo $GIT_COMMIT_REV"
                        //sh "sed -E -i'' "s/(.*nightwolf:).*/\1${GIT_COMMIT_REV}/" app/deployment.yaml"
                        sh "cat app/deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        //sh 'git push https://github.com/samehpalas/argo-cd.git HEAD:main'
                        //sh "git push origin main"
                        sh "git push https://${USER}:${PASS}@github.com/${USER}/argo-cd.git HEAD:main"
                      
      }
    }
  }
}
}
