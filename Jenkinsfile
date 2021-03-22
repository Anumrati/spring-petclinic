node ("jenkins-java"){
    stage ("Checkout pipelines") {
    checkout scm
    checkout (scm: [$class: 'GitSCM',
                    branches: [[name: '*/master']],
                    extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'help_files']],
                    userRemoteConfigs: [[credentialsId: 'Github', url: 'https://github.com/Anumrati/cicd.git']]])
    }
    try {

        load("help_files/jenkinsfiles/jdk/prepare_env.groovy").stages()
        load("help_files/jenkinsfiles/jdk/builder.groovy").stages()
        load("help_files/jenkinsfiles/global/build_docker_push_to_repo.groovy").stages()

    } catch (err) {

        load("help_files/jenkinsfiles/global/exception_handling.groovy").stages(err)

    } finally {

    }
}
