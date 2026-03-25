pipeline{
  agent any
    environment{
      IAMGE_NAME="node-app"
    }
    
    stages{
      stage('clone code'){
        steps{
          echo "cloning repo.."
        }
      }

      stage('Build Docker Iamage'){
        steps{
          echo "building docker image"
          sh "docker build -t ${IAMGE_NAME} ."
        }
      }

      stage('Verify Image'){
        steps{
          echo "listing images"
          sh "docker images"
        }
      }
    }
  }
        
        
    
