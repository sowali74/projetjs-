pipeline {
    agent{
        label 'agent_node'
    }
    environment{
        DOCKER_HUB_PAT = credentials('docker_hub_pat')
    }

    stages {
        stage('clone') {
            steps {
                git branch: 'main', url: 'https://github.com/fredericEducentre/reactJS.git'
            }
        }
        stage('build'){
            steps{
                sh '''
                    npm install
                    npm run build
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }
        stage('Delivery'){
            steps{
                sh 'docker login -u ali957 -p ${DOCKER_HUB_PAT}'
                sh 'docker build . -t ali957/calcul_chauffage:${BUILD_ID}'
                sh 'docker push ali957/calcul_chauffage:${BUILD_ID}'
            }
        }
       
    }
}