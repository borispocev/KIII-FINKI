node {
    def app
    stage('Clone repository') {
        steps {
                git credentialsId: 'github-bp', url: 'https://github.com/borispocev/KIII-FINKI', branch: 'main'
            }
    }
    stage('Build image') {
       app = docker.build("borispocev/KIII-FINKI")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
