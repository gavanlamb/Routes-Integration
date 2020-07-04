 def AWS_ARTIFACT_BUCKET_REGION = "ap-southeast-2"
 def AWS_CREDENTIALS_ID = "Haplo-Tech-AWS"
 pipeline {
     agent any
     stages {
         stage("Update stack") {
             when {
                 expression {
                     GIT_BRANCH = "origin/" + sh(returnStdout: true, script: "git rev-parse --abbrev-ref HEAD").trim()
                     return GIT_BRANCH == "origin/master"
                 }
             }
             steps {
                 withAWS(region:"${AWS_ARTIFACT_BUCKET_REGION}", credentials:"${AWS_CREDENTIALS_ID}") {
                     cfnUpdate(stack:'haplo-routes-integration', file:'./template.yaml')
                 }
             }
         }
     }
 }