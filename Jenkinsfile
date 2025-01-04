pipeline {
    agent any
    stages {
       stage('Checkout') {
           steps {
               cleanWs()
                git url: 'https://github.com/eijlnuv/Tubes-DevSecOps.git', branch: 'master'
                }
           }
           stage('Build Node.js') {
               steps {
                   sh 'npm install'
                    sh 'npm run build'
                   }
              }
           stage('Deploy to EC2') {
             steps {
               sshPublisher (publishers: [sshPublisherDesc (configName: 'nama-koneksi-ssh', transfers: [sshTransfer (cleanRemote: false, excludes: '', execCommand: 'sudo systemctl restart apache2', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, remoteDirectory: '/var/www/html', removePrefix: '', sourceFiles: './build/**/*')], usePromotion: false, useWorkspaceInPromotion: false)])
             }
          }
       }
}
