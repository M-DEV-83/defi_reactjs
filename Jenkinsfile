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
        stage('build') {
            steps {
                sh'''
                npm install
                npm run build
                '''
            }
        }
        stage('test') {
            steps {
                sh'npm run test'
            }
        } 
        stage('Delivery') {
            steps {
                sh'docker login -u mahnio -p ${DOCKER_HUB_PAT}'
                sh'docker build . -t mahnio/calcul_chauffage:${BUILD_ID}'
                sh'docker push mahnio/calcul_chauffage:${BUILD_ID}'
            }
        } 
        
    }
}
