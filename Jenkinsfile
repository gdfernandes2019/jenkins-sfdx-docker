#!/usr/bin/env groovy

pipeline {
    agent {
        docker {
            image 'sfdx-docker:latest'
        }
    }
    stage('Main build') {
        checkout scm

        stage("SFDX Authentication") {
            sh "sfdx force:auth:jwt:grant --clientid <client-id> --jwtkeyfile certificates/server.key --username <user-name> --instanceUrl https://test.salesforce.com"
        }
        stage("SFDX Deploy") {
            sh "sfdx force:source:convert -d mdapi"
            sh "sfdx force:source:deploy -d mdapi -u <user-name>"
        }
    }
}