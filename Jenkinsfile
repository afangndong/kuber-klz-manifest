node{
    def app

    stage('Clone Repository'){

        checkout scm
    }

    stage('Update GIT'){
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    //def encodePAssword = URL.encode("$GIT_PASSWORD", 'UTF-8')
                    sh "git config user.email clemsbrass@yahoo.fr"
                    sh "git config user.name 'Clement Afang Ndong'"

                    //git switch to master
                    sh "cat deployment.yaml"
                    sh "sed -i 's+afangndong/test.*+afangndong/test:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kuber-klz-manifest.git HEAD:main"
                }
            }
        }
    }
}