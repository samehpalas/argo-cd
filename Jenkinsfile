node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }
    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'sameh-github-cred', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh 'git config --global user.email "samehpalas33@gmail.com" '
                        sh 'git config --global user.name "samehpalas"'
                        //sh 'git remote set-url origin https://${USER}:${PASS}@github.com/samehpalas/argo-cd.git'
                        //sh "git switch master"
                        sh "cat app/deployment.yaml"
                        sh "sh artifact_version_update app/deployment.yaml"
                        sh "echo $GIT_COMMIT_REV"
                        //sh "sed -E -i'' "s/(.*nightwolf:).*/\1${GIT_COMMIT_REV}/" app/deployment.yaml"
                        sh "cat app/deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${encodedPassword}@github.com/${GIT_USERNAME}/argo-cd.git HEAD:main"
                    }
                }
            }
    }
}
   
