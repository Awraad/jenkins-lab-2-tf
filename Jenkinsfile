pipeline {
  agent {
    docker {
      image "bryandollery/terraform-packer-aws-alpine"
      args "-u root --entrypoint='' --rm"
    }
  }
  environment {
    CREDS = credentials('Awraad-aws-creds')
    AWS_ACCESS_KEY_ID = "${CREDS_USR}"
    AWS_SECRET_ACCESS_KEY = "${CREDS_PSW}"
    OWNER = "awraad"
    PROJECT_NAME = 'web-server'
    AWS_PROFILE="kh-labs"
    TF_NAMESPACE="awraad"
  }
  stages {
      stage("init") {
          steps {
              sh 'make init'
          }
      }
      stage("workspace") {
          steps {
              sh """ 

terraform workspace new jenkins-lab-2

terraform workspace select jenkins-lab-2
fi
"""
          }
      }
      stage("plan") {
          steps {
              sh 'make plan'
          }
      }
      stage("apply") {
          steps {
              sh 'make apply'
          }
      }
  }
}
