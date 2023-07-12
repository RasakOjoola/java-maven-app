#!/usr/bin/env groovy

library identifier: 'myJenkins-shared-lib@master', retriever:modernSCM(
        [$class:'GitSCMSource',
         remote: 'https://gitlab.com/Rasakii/myjenkins-shared-library.git',
         credentialsId: 'gitlab-credential'

         ]
)

def gv


pipeline {
    agent any
    tools {
        maven 'maven-3.6'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    buildImage 'rasakojoola/my-repo:jma-3.0'
                    dockerLogin()
                    dockerPush 'rasakojoola/my-repo:jma-3.0'
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
