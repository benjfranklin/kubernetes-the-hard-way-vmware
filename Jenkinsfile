podTemplate(containers: [
    containerTemplate(
        name: 'ansible', 
        image: 'benjfranklin/jenkins-agent-ansible:1.4',
        command: 'sleep', 
        args: '5m'
        )
  ]) {

    node(POD_LABEL) {
        stage('Configure kubernetes nodes') {
            container('ansible') {
                
                stage('Checkout Git repository') {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/benjfranklin/kubernetes-the-hard-way-vmware.git']])
                }
                
                stage('Configure kubernetes master node') {
                    withCredentials([string(credentialsId: 'jenkins-sudo-password', variable: 'password')]) {
                        ansiblePlaybook(credentialsId: 'jenkins', hostKeyChecking: false, inventory: 'ansible/inventories/hosts', playbook: 'ansible/playbooks/k8s-master.yml', extraVars: [ansible_become_password: '$password'])
                    } 
                }

                stage('Configure kubernetes worker nodes') {
                    withCredentials([string(credentialsId: 'jenkins-sudo-password', variable: 'password')]) {
                        ansiblePlaybook(credentialsId: 'jenkins', hostKeyChecking: false, inventory: 'ansible/inventories/hosts', playbook: 'ansible/playbooks/k8s-workers.yml', extraVars: [ansible_become_password: '$password'])
                    } 
                }
                
            }
        }

    }
}
