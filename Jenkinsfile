#!/usr/bin/groovy
pipeline {
    agent any
    environment {
        LANG = "en_US.UTF-8"
    }
    stages {
        stage ('Publish') {
            //steps {
                //step (
                //sshagent([GitHubSSH]) {
                    sh """#!/bin/sh
                    source /opt/rh/rh-python36/enable
                    python3 -m venv $HOME/venv
                    source #HOME/venv/bin/activate
                    pip install --requirement=requirements.txt
                    mkdocs gh-deploy
                    """
                   // }
                //)
            //}
        }
    }
}