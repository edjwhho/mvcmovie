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
            }
        }
        stage('Build Other pipeline') {
            steps {
                script {
                    def built = build(
                        job:'testing-PR',
                    )
                    copyArtifacts(
                        projectName: 'testing-PR',
                        selector: specific("${built.number}"),
                        target: "${env.WORKSPACE}/",
                        filter: "output/*"
                    )
                }
                sh "pwd && tree"
            }

        }
    }
}