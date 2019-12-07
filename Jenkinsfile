node {
  def app
  def versionnum
  stage('Clone repository') {
    checkout scm
 
  } 
  stage('Build image') {
    sh 'pwd'
    app = docker.build("petclinicimage")
  
  }
  stage('Push image') {
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
      app.push("${env.BUILD_NUMBER}")
    }
  }
  stage('Deploy') {
    sh '/usr/local/bin/helm upgrade --install petclinic /var/lib/jenkins/petclinic/ --recreate-pods --set image.repository=https://registry.hub.docker.com --set image.tag=${BUILD_NUMBER}'
  }
}