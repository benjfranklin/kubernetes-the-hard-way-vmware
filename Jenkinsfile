podTemplate(containers: [
    containerTemplate(
        name: 'ansible', 
        image: 'benjfranklin/jenkins-agent-ansible:1.4',
        command: 'sleep', 
        args: '5m'
        )
  ]) {

    node(POD_LABEL) {
        stage('Testing Ansible Agent') {
            container('ansible') {
                stage('Run ansible') {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/benjfranklin/kubernetes-the-hard-way-vmware.git']])
                    sh '''
                        export ANSIBLE_HOST_KEY_CHECKING=False
                    '''
                    withCredentials([string(credentialsId: 'jenkins-sudo-password', variable: 'password')]) {
                        ansiblePlaybook(credentialsId: 'jenkins', hostKeyChecking: false, inventory: 'ansible/inventories/hosts', playbook: 'ansible/playbooks/test.yml', extraVars: [ansible_become_password: '$password'])
                    }
                    
                }
            }
        }

    }
}
