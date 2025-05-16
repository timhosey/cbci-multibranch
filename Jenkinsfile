podTemplate(label: 'k8s-agent', containers: [
    containerTemplate(name: 'alpine', image: 'alpine:3.18', command: 'cat', ttyEnabled: true)
]) {
  node('k8s-agent') {
    stage('Checkout') {
      checkout scm
    }

    stage('Branch-Specific Logic') {
      container('alpine') {
        env.ALLOW_CONCURRENT_BUILDS = allowConcurrentBuilds()
        stage('Example Stage') {
          // Your pipeline steps here
          echo "Concurrent builds: ${String.valueOf(env.ALLOW_CONCURRENT_BUILDS)}"
          echo 'Executing pipeline steps'
          sh "sleep 10"
        }
      }
    }
  }
}

def allowConcurrentBuilds() {
  if (env.BRANCH_NAME != 'main') {
    properties([disableConcurrentBuilds(abortPrevious:true)])
    return false
  } else{
    properties([])
    return true
  }
}