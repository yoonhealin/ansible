# Ansible 실행

```
$ ansible-playbook -i hosts site.yml

PLAY [플레이북 튜토리얼] **********************************************************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************************************************************
ok: [127.0.0.1]

TASK [nginx : libselinux-python과 EPEL 리포지토리 설치] ***************************************************************************************************************
[DEPRECATION WARNING]: Invoking "yum" only once while using a loop via squash_actions is deprecated. Instead of using a loop to supply multiple items and
specifying `name: "{{ item }}"`, please use `name: ['libselinux-python', 'epel-release']` and remove the loop. This feature will be removed in version 2.11.
Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [127.0.0.1] => (item=[u'libselinux-python', u'epel-release'])

TASK [nginx : nginx 설치] ***************************************************************************************************************************************
ok: [127.0.0.1]

TASK [nginx : nginx 서비스 시작과 자동 시작 설정] *************************************************************************************************************************
ok: [127.0.0.1]

TASK [nginx : nginx.conf 템플릿 활용] ******************************************************************************************************************************
changed: [127.0.0.1]

TASK [nginx : 엔진엑스용 그룹 작성] ************************************************************************************************************************************
ok: [127.0.0.1]

TASK [nginx : 엔진엑스용 사용자 작성] ***********************************************************************************************************************************
changed: [127.0.0.1]

RUNNING HANDLER [nginx : 엔진엑스 리로드] ****************************************************************************************************************************
changed: [127.0.0.1]

PLAY RECAP ****************************************************************************************************************************************************
127.0.0.1                  : ok=8    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```