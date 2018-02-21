#!groovy

node('master') {

    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

          checkout scm
       }

       stage('Pre-Build'){

        
       }

       stage('Build'){

         env.NODE_ENV = "build"

         print "Environment will be : ${env.NODE_ENV}"
         sh('sudo ./build.sh')

       }

       stage('Publish'){

         echo 'Push to Repo'
         dir('.') {
          sh 'ARTIFACT_LABEL=bronze ./dockerPushToRepo.sh'
          sh './src/app/metadata.sh > metadata.json'
          sh 'cat metadata.json'
          archive includes: "metadata.json"
         }

       }
    }
    catch (err) {
        currentBuild.result = "FAILURE"
        throw err
    }

}
