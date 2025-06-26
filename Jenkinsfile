pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            sh(script: 'docker compose build')
            echo "building docker container..."
         }
      }
      stage('Start App') {
         steps {
            sh(script: 'docker compose up -d')
            echo "starting app"
         }
      }
      stage('Run Tests') {
         steps {
            sh(script: 'pytest ./tests/test_sample.py')
         }
         post {
            success {
               echo "Tests passed! :)"
            }
            failure {
               echo "Tests failed :("
            }
         }
      }
   }
   post {
      always {
         sh(script: 'docker compose down')
         echo "closing docker container..."
      }
   }
}
