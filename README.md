# Jenkins

## Jenkins Plugins

Um die Jenkins Plugins richtig auszuwählen, musste ich wissen, wie die selbigen heissen. Der Link hier
<https://updates.jenkins.io/download/plugins/> war extrem hilfreich. Die Pluginnamen entsprechen den Ordnernamen.

## Start by ansible

 `ansible-playbook --key-file "ssh-keys/id_rsa" nodes-setup.yml`

## bekannte Fehler

```bash
TASK [jenkinsmaster : Create User] **************************************************************************************************************************
fatal: [jenkinsmaster]: FAILED! => {"changed": true, "cmd": "echo 'hpsr=new hudson.security.HudsonPrivateSecurityRealm(false); hpsr.createAccount(\"dummyuser\", \"dummypassword\")' | java -jar /var/lib/jenkins/jenkins-cli.jar -s http://localhost:8080 groovy =", "delta": "0:00:00.471110", "end": "2018-06-10 20:29:00.895887", "msg": "non-zero return code", "rc": 6, "start": "2018-06-10 20:29:00.424777", "stderr": "\nERROR: anonymous is missing the Overall/Read permission", "stderr_lines": ["", "ERROR: anonymous is missing the Overall/Read permission"], "stdout": "", "stdout_lines": []}
to retry, use: --limit @/Users/Silversurfer/git-projects/ansible-jenkins/setup-jenkins.retry
```

-> Einfach nochmal ausführen, scheint ein vorübergehender Fehler zu sein

Link für Credentials
<https://getintodevops.com/blog/how-to-add-jenkins-credentials-with-curl-or-ansible>

## Tasks

die Security ist noch nicht wieder aktiviert nach der Plugin installation.
Eventuell kann man hier die einzelnen Playbooks noch verschieben.

Der Username/Password werden noch nicht aus den Variablen gelesen.

Vielleicht kann man die Replaces noch mit XML ersetzen.