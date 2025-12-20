pipeline {
    agent any
     environment {
        DOCKERHUB = credentials('dockerhub')
        SONAR_TOKEN = credentials('sonar-token-id')
         
    }

    stages {
        
        stage('Checkout GitHub') {
            steps {
                git branch: 'master', url: 'https://github.com/oumaya-khemir/spring-boot-angular-example.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('server') {
                    sh 'mvn package -DskipTests'
                }
            }
        }
        stage('SonarQube Analysis - Backend') {
            steps {
                dir('server') { // dossier Spring Boot
                    withCredentials([string(credentialsId: 'sonar-token-id', variable: 'SONAR_TOKEN')]) {
                        sh '''
                            mvn clean verify sonar:sonar \
                                -DskipTests \
                                -Dsonar.projectKey=backend \
                                -Dsonar.projectName="Backend Spring Boot" \
                                -Dsonar.host.url=http://192.168.56.103:9000 \
                                -Dsonar.login=${SONAR_TOKEN} \
                                -Dsonar.java.binaries=target/classes
                '''
            }
        }
    }
}
        
       /* stage('SonarQube Analysis') {
            steps {
                dir('server') {
                    withCredentials([string(credentialsId: 'sonar-token-id', variable: 'SONAR_TOKEN')]) {
                    sh(
                        label: 'Run Sonarqube Scanner',
                        script: '''
                        docker run --rm \
                            --network sonarnet \
                            -e SONAR_HOST_URL=http:192.168.56.103:9000 \
                            -e SONAR_LOGIN="$SONAR_TOKEN" \
                            -v "${WORKSPACE}/server"\
                            sonarsource/sonar-scanner-cli
                            '''
                    )
                    }
        }
    }
} */

       /* stage('Build Frontend') {
            steps {
                dir('client') {
                    sh 'npm install --legacy-peer-deps'
                    sh 'npm run build --prod'
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                sh 'docker build -t server:latest server/'
                sh 'docker build -t client:latest client/'
            }
        }
        

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin'
            }
        }

        stage('Push Docker Images') {
            steps {
                sh 'docker tag server:latest $DOCKERHUB_USR/server:latest'
                sh 'docker tag client:latest $DOCKERHUB_USR/client:latest'

                sh 'docker push $DOCKERHUB_USR/server:latest'
                sh 'docker push $DOCKERHUB_USR/client:latest'
            }
        }
        */

    }
}
