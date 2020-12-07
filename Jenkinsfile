pipeline {
    agent any

    stages {
        stage('Making dir') {
            steps {
                echo 'Creating..'
               // Make the output directory.
                sh "mkdir -p output"
            }
        }
        stage('Writing files') {
            steps {
                echo 'Write..'
                // Write an useful file, which is needed to be archived.
                writeFile file: "output/usefulfile.txt", text: "This file is useful, need to archive it."
                // Write an useless file, which is not needed to be archived.
                writeFile file: "output/uselessfile.md", text: "This file is useless, no need to hive it."
            }
        }
        stage('Creating artifact') {
            steps {
                echo 'Archive build output....'
                // Archive the build output artifacts.
                archiveArtifacts artifacts: 'output/*.txt', excludes: 'output/*.md', fingerprint: true
                // stashking same file
                stash includes: 'output/*', name: 'usefulfile.txt'
            }
        }

        stage('Unstashing') {
            steps {
               unstash 'usefulfile.txt'
               sh "ls -l"
               sh "cat output/usefulfile.txt"
            }
        }
        stage ('push artifact') {
            steps {
                sh 'mkdir archive'
                sh 'echo testing zipping and archiving files > archive/test.txt'
                sh 'zip -r test.zip archive'
                archiveArtifacts artifacts: 'test.zip', fingerprint: true
            }
        }

    }
}