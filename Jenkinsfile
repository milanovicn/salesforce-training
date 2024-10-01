pipeline {
    agent any
    environment {
        HUB_ORG = ${env.HUB_ORG_DH}
        SFDC_HOST = ${env.SFDC_HOST_DH}
        JWT_KEY_CRED_ID = ${env.JWT_CRED_ID_DH}
        CONNECTED_APP_CONSUMER_KEY = ${env.CONNECTED_APP_CONSUMER_KEY_DH}
    }
    stages {
        stage("List variables") {
            steps {
                    sh"""
                        echo "HUB_ORG: $HUB_ORG"
                        echo "SFDC_HOST: $SFDC_HOST"
                        echo "JWT_KEY_CRED_ID: $JWT_KEY_CRED_ID"
                        echo "CONNECTED_APP_CONSUMER_KEY: $CONNECTED_APP_CONSUMER_KEY"
                    """
            }
        }
    }
}
