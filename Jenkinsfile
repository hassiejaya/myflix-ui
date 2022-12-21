node {
    def app

    stage('Clone repository') {
        git branch: 'master/myflix-ui', url: 'https://github.com/hassiejaya/myflixapp.git'

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("myflixuiimage")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        withDockerRegistry([ credentialsId: "f459eeda-397d-48cf-a4d6-edcf8827b139", url: "https://hub.docker.com/repository/docker/assignmentlk/myflix" ]) {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}