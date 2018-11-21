node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    /*stage('Build Docker test'){
     sh 'docker build -t react-test -f Dockerfile.test --no-cache .'
    }
    stage('Docker test'){
      sh 'docker run --rm react-test'
    }
    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    }*/
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t react-app --no-cache .'
        sh 'docker tag react-app localhost:5000/react-app'
        sh 'docker push localhost:5000/react-app'
        sh 'docker rmi -f react-app localhost:5000/react-app'
          
        // Remove old image and deploy new image on container
        sh 'docker pull localhost:5000/react-app'
        sh 'docker stop emojisearchapp'
        sh 'docker rm emojisearchapp'
        sh 'docker run -d -p 3000:3000 --name emojisearchapp localhost:5000/react-app:latest'
      }
    }
  }
  catch (err) {
    throw err
  }
}
