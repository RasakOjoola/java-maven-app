#!/usr/bin/env groovy

@Library('myJenkins-shared-lib')
def gv

pipeline {
    agent any
    tools {
        maven 'Maven'
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
                     //echo "building jar"
                     // gv.buildJar()
                      buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                     buildImage()
                     //echo "building image"
                     // gv.buildImage()
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                    gv.deployApp()
                }
            }
        }
    }
}
