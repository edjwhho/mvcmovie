pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Creating..'
               // Make the output directory.
                sh "mkdir -p output"
            }
        }
        stage('Test') {
            steps {
                echo 'Write..'
                // Write an useful file, which is needed to be archived.
                writeFile file: "output/usefulfile.txt", text: "This file is useful, need to archive it."
                // Write an useless file, which is not needed to be archived.
                writeFile file: "output/uselessfile.md", text: "This file is useless, no need to arc:w
                hive it."
            }
        }
        stage('Deploy') {
            steps {
                echo 'Archive build output....'
                // Archive the build output artifacts.
                archiveArtifacts artifacts: 'output/*.txt', excludes: 'output/*.md'
            }
        }
  
}