node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'ca0bdb6b-4470-45f4-baef-259619495ab8', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "cd ${APP_NAME}"
			sh "git config user.email contact@feketegabor.com"
                        sh "git config user.name gaborfekete85"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+gabendockerzone/test-devops.*+gabendockerzone/test-devops:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/devops-manifest.git HEAD:master"
      }
    }
  }
}
}
