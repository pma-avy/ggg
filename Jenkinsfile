pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        script {
          properties([parameters([choice(choices: ['61', '62'], description: '', name: 'ENV1')])])
        }

        echo "${ENV1}"
      }
    }
    stage('checkout') {
      parallel {
        stage('checkout') {
          steps {
            git(url: 'https://github.com/royalaluf/pmx_packages.git', branch: 'master', credentialsId: '0340ec58-386d-4b88-a16d-26611b92e224')
          }
        }
        stage('checkout') {
          steps {
            git(url: 'https://github.com/royalaluf/envloader.git', credentialsId: '0340ec58-386d-4b88-a16d-26611b92e224', branch: 'new_vpc')
          }
        }
      }
    }
    stage('cloudformation') {
      steps {
        cfnUpdate(stack: 'ELStg-"${ENV1}"', create: true, file: 'CFStack_ELSTG.txt', params: 'PreDns=autoenv-${ENV1};EnvName=ELStg-${ENV1};ScriptsGitTag=${SCRIPTS};SnGenGitTag=${SNGENERATOR_GIT_TAG};NBLGitTag=${NEARBYLOCATION_GIT_TAG};OpSvrGuiGitTag=${OPSVR_GUI_GIT_TAG};GwFeGitTag=${GWFE_GIT_TAG};CouponsGitTag=${COUPONS_GIT_TAG};AppFeGitTag=${APPFE_GIT_TAG};WsGwFeGitTag=${WS_GW_FE_GIT_TAG};PermissionGitTag=${PERMISSION_GIT_TAG};OpSvrApiGitTag=${OPSVRAPI_GIT_TAG};AuthenticationGitTag=${AUTHENTICATION_GIT_TAG};OpSvrGitTag=${BACKOFFICE_GIT_TAG};DownloadFwVersionsGitTag=${DOWNLOAD_FW_VERSIONS};EncryptMongoHost=${EncryptMongoHost};DownloadFwVersionsGitTag=${DownloadFwVersionsGitTag}', timeoutInMinutes: 900)
      }
    }
  }
}