pipeline {
    agent any
    environment {
        HUB_ORG = "${env.HUB_ORG_DH}"
        SFDC_HOST = "${env.SFDC_HOST_DH}"
        JWT_KEY_CRED_ID = "${env.JWT_CRED_ID_DH}"
        CONNECTED_APP_CONSUMER_KEY = "${env.CONNECTED_APP_CONSUMER_KEY_DH}"
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
        stage("List variables") {
            steps {
                withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'jwt_key_file')]) {
                    echo "*** Authorizing hub org ***"
                    script {
                        rc = sh returnStatus: true, script: "${toolbelt} auth:jwt:grant -i ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} -f ${jwt_key_file} -r ${SFDC_HOST} -d"
                        if (rc != 0) { 
                            println 'inside rc 0'
                            error 'hub org authorization failed' 
                        }
                        else {
                            println 'rc not 0'
                        }
                        print 'rc value:'
                        println rc
		
                    }
                }
            }
        }
    }
}
