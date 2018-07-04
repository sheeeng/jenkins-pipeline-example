#!/usr/bin/env groovy

println "Hello from Jenkinsfile!"

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building.'
                library identifier: 'westeros@master', retriever: modernSCM([$class: 'GitSCMSource', credentialsId: '', id: 'a7037fe6-c0fb-4416-961c-61a6ba5c8aaf', remote: 'https://github.com/sheeeng/jenkins-pipeline-library-example', traits: [[$class: 'jenkins.plugins.git.traits.BranchDiscoveryTrait']]])
                script {
                    for (i = 0; i <5; i++) {
                        showRandomWesterosStory()
                        sleep(1)
                    }
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing.'

                script {
                    timeout(time: 30, unit: 'SECONDS') {
                        def userInputResult = input(
                            id: "userInput",
                            submitter: 'administrator,jon,daenerys',
                            submitterParameter: 'submitter',
                            message: "Are you sure to proceed?",
                            parameters: [
                                [$class: 'TextParameterDefinition',
                                    name: 'customText',
                                    defaultValue: "What's on your mind?",
                                    description: "What's on your mind?"],
                                [$class: 'BooleanParameterDefinition',
                                    name: 'customBoolean',
                                    defaultValue: false,
                                    description: 'Are you sure what are you doing?']
                        ])
                        echo "It was `${userInputResult.submitter}` who submitted the dialog."
                        echo "Received `${userInputResult.customText}` as submitted custom text parameter."
                        echo "Received `${userInputResult.customBoolean}` as submitted custom boolean parameter."
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying.'
            }
        }
    }
}

