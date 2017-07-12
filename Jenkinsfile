#!groovy

node('docker') {

    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

          checkout scm
       }

       stage('Pre-Build'){

         sh('./installDeps.sh')

       }

       stage('Build'){

         env.NODE_ENV = "build"

         print "Environment will be : ${env.NODE_ENV}"
         sh('./build.sh')

       }

       stage('Publish'){

         echo 'Push to Repo'
         sh 'ls -al ~/'
         sh 'ARTIFACT_LABEL=bronze ./dockerPushToRepo.sh'

       }

       stage('Deploy to Dev'){

         sh 'ARTIFACT_LABEL=bronze ENV=dev ./deploy.sh'

       }
    }
    catch (err) {
        currentBuild.result = "FAILURE"
        throw err
    }

}