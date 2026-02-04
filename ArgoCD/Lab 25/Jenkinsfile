pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = 'nouraabdelnabi'
        REPO_NAME       = 'jenkins-app'
        IMAGE_NAME      = "${DOCKER_HUB_USER}/${REPO_NAME}"
        IMAGE_TAG       = "${env.BUILD_NUMBER}"
        GITHUB_REPO_URL = 'github.com/noura-abdelnabi/argocd-lab-deploy.git'
    }

    stages {
        stage('Maven Build') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build & Push Docker Image') {
            steps {
                script {
                    // 1. Build & 2. Build Docker Image
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                    
                    // 3. Push image to Docker hub
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                    }
                }
            }
        }

        stage('Clean Up & Update Manifest') {
            steps {
                script {
                    // 4. Delete image locally
                    sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"

                    // 5. Edit new image in deployment.yaml file
                    sh "sed -i 's|image:.*|image: ${IMAGE_NAME}:${IMAGE_TAG}|' k8s/deployment.yaml"
                }
            }
        }

        stage('Push to GitHub') {
            steps {
                script {
                    // 6. Push new update files into Github repo
                    withCredentials([usernamePassword(credentialsId: 'github-token', passwordVariable: 'TOKEN', usernameVariable: 'USER')]) {
                        sh "git config user.email 'jenkins@example.com'"
                        sh "git config user.name 'Jenkins CI'"
                        sh "git add k8s/deployment.yaml"
                        sh "git commit -m 'Update image tag to ${IMAGE_TAG} [skip ci]'"
                        sh "git push https://${USER}:${TOKEN}@${GITHUB_REPO_URL} HEAD:main"
                    }
                }
            }
        }
    }
}


