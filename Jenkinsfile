def BRANCH = env.BRANCH_NAME
def TAG = BRANCH.split('-')[1]
def SVC_NAME = "getsvcname"
def releaseName = "${SVC_NAME}"
def CREDENTIALS_ID = "gitcred"
def GIT_REPO = "giturl"
pipeline {
    agent any

    environment {
        // Set your Kubernetes context and namespace
        KUBECONFIG = '/var/lib/jenkins/config'
        KUBE_NAMESPACE = 'nmspace'
    }

    stages {
        stage("Clean Workspace") {
            steps {
                  cleanWs()
            }
        }
        stage("Git") {
            steps { 
                git branch: "${BRANCH}", credentialsId: "${CREDENTIALS_ID}", url: "${GIT_REPO}"
            }
        }
        stage('Git checkout') {
            steps {
                script{
                    sh label: '', script: "git checkout "
                }
            }
        }
        stage('Deploy Helm Chart') {
            steps {
                script {
                    // Set the Helm chart path and release name
                    def helmChartPath = "${env.WORKSPACE}/${SVC_NAME}"
                    // Deploy the Helm chart
                    sh """
                        helm upgrade --install ${releaseName} ${helmChartPath} --namespace ${KUBE_NAMESPACE} --kubeconfig ${KUBECONFIG}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}

