node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }
    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'sameh-github-cred', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh 'git --global config user.email "samehpalas33@gmail.com" '
                        sh 'git --global config user.name "samehpalas"'
                        sh 'git remote set-url origin https://${USER}:${PASS}@github.com/samehpalas/argo-cd.git'
                        //sh "git switch master"
                        sh "cat app/deployment.yaml"
                        sh "sh artifact_version_update app/deployment.yaml"
                        sh "echo $GIT_COMMIT_REV"
                        //sh "sed -E -i'' "s/(.*nightwolf:).*/\1${GIT_COMMIT_REV}/" app/deployment.yaml"
                        sh "cat app/deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push origin HEAD:main"
                    }
                }
            }
    }
}
   
