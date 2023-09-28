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
                    steps {
                        git 'https://github.com/benjfranklin/kubernetes-the-hard-way-vmware.git'
                        sh '''
                            whoami
                            pwd
                            ls -la
                        '''
                        sh 'kubernetes-the-hard-way-vmware'
                        ansiblePlaybook(credentialsId: 'jenkins', inventory: 'kubernetes-the-hard-way-vmware/ansible/inventories/hosts', playbook: 'ansible/playbooks/test.yml')
                    }
                }
            }
        }

    }
}
