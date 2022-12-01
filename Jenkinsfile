pipeline {

  agent any
  
  environment{
  ANYPOINT_CRED = credentials('ANYPOINT_CREDENTIALS')
  }
  
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          echo "******** Munit test cases execution********"
      }
    }

     stage('Deployment') {
     environment{
  			CLIENT_ID = credentials('DEV_CLIENT_ID')
  			CLIENT_SECRET = credentials('DEV_CLIENT_SECRET')
  		}
      steps {
            bat 'mvn -U -V -e -B -DskipTests -Pdev deploy -DmuleDeploy -Danypoint.username="%ANYPOINT_CRED.USR%" -Danypoint.password="%ANYPOINT_CRED.PSW%" -Danypoint.platform.client_id="%CLIENT_ID%" -Danypoint.platform.client_secret="%CLIENT_SECRET%"'
      }
    }
  }
}