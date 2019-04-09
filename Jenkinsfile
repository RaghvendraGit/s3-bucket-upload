pipeline {
   agent any
   environment {
       ENV_NAME = "${env.BRANCH_NAME}"
   }
   parameters {
       choice(name: 'Env', choices: ['Dev', 'Prod'], description: 'Select Deploy Environment')
   }

   stages {
       stage('Deploy Dev') {
           when {
               expression { ENV_NAME == 'master' && params.Env == 'Dev'}
               }
               steps {
                sh("aws s3 sync . s3://devtest2308 --delete --exclude '.git*' --exclude 'Jenkinsfile' --dryrun")
               }
           }

       stage('Deploy Prod') {
           when {
               expression {ENV_NAME == 'master' && params.Env == 'Prod'}
               }
               steps {
               sh("aws s3 sync . s3://prodtest2308  --delete --exclude '.git*' --exclude 'Jenkinsfile' --dryrun")
               }
           }
       }
}
