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
                sh("aws s3 sync . s3://executivedashboard.dev.pgac.io --delete --exclude '.git*' --exclude 'Jenkinsfile' --profile dev-virginia --dryrun")
               }
           }

       stage('Deploy Prod') {
           when {
               expression {ENV_NAME == 'master' && params.Env == 'Prod'}
               }
               steps {
               sh("aws s3 sync . s3://data.pgac.com  --delete --exclude '.git*' --exclude 'Jenkinsfile' --profile prod-virginia --dryrun")
               }
           }
       }
}