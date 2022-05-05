pipeline {
  agent {
    kubernetes {
      label 'promo-app'  // all your pods will be named with this prefix, followed by a unique id
      idleMinutes 5  // how long the pod will live after no jobs have run on it
      yamlFile 'build-agent.yaml'  // path to the pod definition relative to the root of our project 
      defaultContainer 'maven'  // define a default container if more than a few stages use it, will default to jnlp container
    }
  }
  environment { 
        APP_NAME = "monorepo-demo"
        registry = "rladkat/demo-service" 
        registryCredential = 'dockerhub_id' 
        dockerImage = '' 
    }
  stages {
    stage('Build') {
      steps {  // no container directive is needed as the maven container is the default
        sh "mvn clean package"   
      }
    }
    stage('Package') {
      agent {
                docker { image 'docker-tools' }
            }
        steps {
          
          sh " ls -al"
          sh " docker --version"
        }
      }
    }
  }
}
