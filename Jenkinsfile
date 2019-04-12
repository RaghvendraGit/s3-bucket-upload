pipeline {
   agent any
   environment {
       ENV_NAME = "${env.BRANCH_NAME}"
   }
   parameters {
       choice(name: 'Env', choices: ['Prod'], description: 'Select Deploy Environment')
   }
   triggers {
    pollSCM('') // Enabling being build on Push
  }
   stages {
       stage('Deploy Dev') {
           when {
               branch ('master')
               }
               steps {
                sh("aws s3 sync . s3://devtest2308 --delete --exclude '.git*' --exclude 'Jenkinsfile'")
               }
           }

       stage('Deploy Prod') {
           when {
               expression {ENV_NAME == 'master' && params.Env == 'Prod'}
               }
               steps {
               sh("aws s3 sync . s3://prodtest2308  --delete --exclude '.git*' --exclude 'Jenkinsfile'")
               }
           }
       }
}
