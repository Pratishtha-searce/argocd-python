pipeline {
    agent any

    stages {
            stage('Update GIT') {
                steps {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: '3c53b0c0-94d8-49df-be80-a8e388d24632', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                            sh "git config user.email pratishtha.agarwal@searce.com"
                            sh "git config user.name Pratishtha-searce"
                            //sh "git switch master"
                            sh 'echo ${GIT_USERNAME}'
                            sh 'echo ${GIT_PASSWORD}'
                            sh "cat ./k8s-manifest/deployment.yaml"
                            //sh 'sed "s/latest/${GIT_COMMIT}/g" ./k8s-manifest/deployment.yaml.sample > ./k8s-manifest/deployment.yaml'
                            //sh 'rm ./k8s-manifest/deployment.yaml.sample'
                            sh "sed -i 's+gcr.io/searce-playground-v1/cicd-python.*+gcr.io/searce-playground-v1/cicd-python:${DOCKERTAG}+g' ./k8s-manifest/deployment.yaml"
                            sh "cat ./k8s-manifest/deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${DOCKERTAG}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-python.git HEAD:main"
                        
                    }
                }
                
            }
        }
    }
}