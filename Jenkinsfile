node {
  label 'centos'
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
    stage('Build Docker test'){
      sh 'docker build -t react-test -f Dockerfile.test --no-cache . '
    }
    /* stage('Docker test'){
      sh 'docker run --rm react-test'
    }
    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    } */
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t puru-react-app --no-cache .'
        sh 'docker tag puru-react-app 7404298959/reacthub:v1.0'
        sh 'docker push 7404298959/reacthub:v1.0'
      }
    }
  }
  catch (err) {
    throw err
  }
}
