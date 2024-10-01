pipeline {
    agent any
    environment {
        HUB_ORG = "${env.HUB_ORG_DH}"
        SFDC_HOST = "${env.SFDC_HOST_DH}"
        JWT_KEY_CRED_ID = "${env.JWT_CRED_ID_DH}"
        CONNECTED_APP_CONSUMER_KEY = "${env.CONNECTED_APP_CONSUMER_KEY_DH}"
        toolbelt = tool 'sf_cli'    
    }
    stages {
        stage("List variables") {
            steps {
                    sh"""
                        echo "*** Printig variables ***"
                        echo "HUB_ORG: $HUB_ORG"
                        echo "SFDC_HOST: $SFDC_HOST"
                        echo "JWT_KEY_CRED_ID: $JWT_KEY_CRED_ID"
                        echo "CONNECTED_APP_CONSUMER_KEY: $CONNECTED_APP_CONSUMER_KEY"
                    """
            }
        }
        stage("Authorize org") {
            steps {
                withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'jwt_key_file')]) {
                    echo "*** Authorizing hub org ***"
                    script {
                        rc = sh returnStatus: true, script: "${toolbelt} org login jwt --client-id ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwt-key-file ${jwt_key_file} --instance-url ${SFDC_HOST}  --set-default-dev-hub"
                        if (rc != 0) {
                            error 'Salesforce dev hub org authorization failed.'
                        }
                    }
                }
            }
        }
        stage('Create Test Scratch Org') {
            steps {
                script {
                    rc = command "${toolbelt} org create scratch --target-dev-hub HubOrg --set-default --definition-file config/project-scratch-def.json --alias testScratch --wait 10 --duration-days 1"
                    if (rc != 0) {
                        error 'Salesforce test scratch org creation failed.'
                    }
                }
            }
        }
    }
}
