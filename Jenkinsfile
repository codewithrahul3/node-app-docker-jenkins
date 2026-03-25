pipeline{
  agent any
    environment{
      IAMGE_NAME="node-app"
      VM_IP="98.93.71.166"
      VM_USER="ubuntu"
      
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

      stage('Save image'){
        steps{
          echo "saving docker image"
          sh "docker save ${IAMGE_NAME} > ${IMAGE_NAME}.tar"
        }
      }

      stage('Copy image to VM'){
        steps{
          sshagent(['VM-CRED']){

            sh """
            scp -o StrictHostKeyChecking=no ${VM_USER}@{VM_IP} '
            docker load < ${IMAGE_NAME}.tar &&
            docker stop node-container || true &&
            docker rm node-container || true &&
            docker run -d -p 3000:3000 --name node-container ${IMAGE_NAME}
            '
            """
          }
        }
      }
    }
  }
        
        
    
