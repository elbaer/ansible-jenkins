# Jenkins

## Jenkins Plugins

Um die Jenkins Plugins richtig auszuwählen, musste ich wissen, wie die selbigen heissen. Der Link hier
<https://updates.jenkins.io/download/plugins/> war extrem hilfreich. Die Pluginnamen entsprechen den Ordnernamen.

## Installation Guide

```bash
vagrant up
ansible-playbook nodes-setup.yml
ansible-playbook jenkinsmaster-setup.yml
ansible-playbook dockerslave-setup.yml
```

## bekannte Fehler

```bash
TASK [jenkinsmaster : Create User] **************************************************************************************************************************
fatal: [jenkinsmaster]: FAILED! => {"changed": true, "cmd": "echo 'hpsr=new hudson.security.HudsonPrivateSecurityRealm(false); hpsr.createAccount(\"dummyuser\", \"dummypassword\")' | java -jar /var/lib/jenkins/jenkins-cli.jar -s http://localhost:8080 groovy =", "delta": "0:00:00.471110", "end": "2018-06-10 20:29:00.895887", "msg": "non-zero return code", "rc": 6, "start": "2018-06-10 20:29:00.424777", "stderr": "\nERROR: anonymous is missing the Overall/Read permission", "stderr_lines": ["", "ERROR: anonymous is missing the Overall/Read permission"], "stdout": "", "stdout_lines": []}
to retry, use: --limit @/Users/Silversurfer/git-projects/ansible-jenkins/setup-jenkins.retry
```

-> Einfach nochmal ausführen, scheint ein vorübergehender Fehler zu sein

## Tasks

Ansible Vault
<https://serversforhackers.com/c/how-ansible-vault-works>

* General Settings -> neue Cloud (Docker) -> mit tcp://ip-docker-slave:4243 verbinden
* Unter dem Punkt 'Pipeline Model Definition' kann man das Label des docker-slaves angeben, da es in der Pipeline nicht möglich ist, den entsprechend Slave anzugeben auf dem gebuildet werden soll

* IPs anhand von inventory/hosts anlegen (dynamische Zuweisung)
* <https://stackoverflow.com/questions/48386717/ansible-slurp-as-private-key-in-jenkins-credential-api-error-for-json-parsing>

https://www.greenreedtech.com/creating-jenkins-credentials-via-the-rest-api/

## Links

Slaves hinzufügen

* <https://support.cloudbees.com/hc/en-us/articles/115003896171-Creating-node-with-Rest-API-and-ManuallyTrustedKeyVerificationStrategy>
* <https://gist.github.com/sergeyhush/4e892837cf5c31c3d242>

Credentials

* <https://getintodevops.com/blog/how-to-add-jenkins-credentials-with-curl-or-ansible>
