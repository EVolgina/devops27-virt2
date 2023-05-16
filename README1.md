# Задача 1
1) Опишите основные преимущества применения на практике IaaC-паттернов.
#### Ответ:
- Скорость и уменьшение затрат: IaC позволяет быстрее конфигурировать инфраструктуру и направлен на обеспечение прозрачности, чтобы помочь другим командам со всего предприятия работать быстрее и эффективнее. Это освобождает дорогостоящие ресурсы для выполнения других важных задач.

- Масштабируемость и стандартизация: IaC предоставляет стабильные среды быстро и на должном уровне. Командам разработчиков не нужно прибегать к ручной настройке - они обеспечивают корректность, описывая с помощью кода требуемое состояние сред. Развертывания инфраструктуры с помощью IaC повторяемы и предотвращают проблемы во время выполнения, вызванных дрейфом конфигурации или отсутствием зависимостей. IaC полностью стандартизирует сетап инфраструктуры, что снижает вероятность ошибок или отклонений.

- Безопасность и документация: Если за провизионирование всех вычислительных, сетевых и служб хранения отвечает код, они каждый раз будут развертываться одинаково. Это означает, что стандарты безопасности можно легко и последовательно применять в разных компаниях. IaC также служит некой формой документации о правильном способе создания инфраструктуры и страховкой на случай, если сотрудники покинут вашу компанию, обладая важной информацией. Поскольку код можно версионировать, IaC позволяет документировать, регистрировать и отслеживать каждое изменение конфигурации вашего сервера.

- Восстановление в аварийных ситуациях: Название говорит само за себя — это очень важно. IaC — чрезвычайно эффективный способ отслеживания вашей инфраструктуры и повторного развертывания последнего работоспособного состояния после сбоя или катастрофы любого рода. Каждый, кто просыпался в 4 часа утра из-за того, что их сайт не работает, скажет вам, что важность быстрого восстановления после того, как ваша инфраструктура вышла из строя, нельзя недооценивать.
2) Какой из принципов IaaC является основополагающим?
- Основопологающим принципом IaaC является идемпотентность - свойство повторять одни и те же действия безошибочно. В контексте систем управления конфигурациями это означает, что сценарии, написанные с соблюдением такого подхода, не изменят, не сломают и не выдадут ошибок на управляемом хосте при повторном запуске.
# Задача 2
1) Чем Ansible выгодно отличается от других систем управление конфигурациями?
Выгодные отличия Ansible от других систем управления конфигурациями:
- быстро осваивается, достаточно поверхностного понимания синтаксиса YAML и Jinja
- нет необходимости устанавливать специальное ПО на хосты, нужен только SSH и python
- подробная и наглядная документация
- большое количество модулей
- позволяет реализовать принцип идемпотентности в управлении состояниями хостов
2) Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?
 - существует два подхода к IaC, декларативный или императивный, и два возможных метода, push и pull. Декларативный подход описывает конечную цель и определяет требуемое состояние ваших ресурсов. Этот подход отвечает на вопрос о том, что нужно создать, например, «Мне нужны две виртуальные машины». Императивный подход отвечает на вопрос о том, как нужно изменить инфраструктуру для достижения конкретной цели, обычно выдавая последовательность различных команд. Разница между методом push и pull заключается в том, каким образом серверам сообщается информация о конфигурации. В pull режиме каждый сервер будет пулить свою конфигурацию из мастер-сервера, а в push режиме мастер-сервер сам распушивает конфигурацию по целевой системе.
 - Прочитавм много материалов, я думаю, что следует использовать то, что больше подходит к конкретному случаю или комбинировать.

# Задача 3
Установите на личный компьютер:

```VirtualBox,
c:\work>vagrant box list
bento/ubuntu-20.04 (virtualbox, 202212.11.0)
```

```Vagrant,
c:\work>vagrant -v
Vagrant 2.3.4
```

```Ansible.
vagrant@server1:~$ ansible --version
ansible [core 2.12.10]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/vagrant/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.8.10 (default, Nov 14 2022, 12:59:47) [GCC 9.4.0]
  jinja version = 2.10.1
  libyaml = True
vagrant@server1:~$ sudo nano /etc/ansible/hosts
vagrant@server1:~$ ansible-inventory --list -y
all:
  children:
    nodes:
      children:
        manager:
          hosts:
            server1.netology:
              ansible_host: 127.0.0.1
              ansible_port: 20011
              ansible_user: vagrant
    ungrouped: {}
    ```
Приложите вывод команд установленных версий каждой из программ, оформленный в Markdown.

Задача 4
Воспроизведите практическую часть лекции самостоятельно.

Создайте виртуальную машину.
Зайдите внутрь ВМ, убедитесь, что Docker установлен с помощью команды

```sudo systemctl status docker
 docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2023-05-16 06:58:23 UTC; 4min 41s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 3930 (dockerd)
      Tasks: 7
     Memory: 23.2M
     CGroup: /system.slice/docker.service
             └─3930 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

May 16 06:58:19 server1 systemd[1]: Starting Docker Application Container Engine...
May 16 06:58:19 server1 dockerd[3930]: time="2023-05-16T06:58:19.998822487Z" level=info msg="Starting up"
lines 1-13...skipping...
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2023-05-16 06:58:23 UTC; 4min 41s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 3930 (dockerd)
      Tasks: 7
     Memory: 23.2M
     CGroup: /system.slice/docker.service
             └─3930 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

May 16 06:58:19 server1 systemd[1]: Starting Docker Application Container Engine...
May 16 06:58:19 server1 dockerd[3930]: time="2023-05-16T06:58:19.998822487Z" level=info msg="Starting up"
May 16 06:58:20 server1 dockerd[3930]: time="2023-05-16T06:58:20.006598540Z" level=info msg="detected 127.0.0.53 nameserver, assuming systemd-resolved, so using resolv>May 16 06:58:21 server1 dockerd[3930]: time="2023-05-16T06:58:21.426464937Z" level=info msg="Loading containers: start."
May 16 06:58:23 server1 dockerd[3930]: time="2023-05-16T06:58:23.360433689Z" level=info msg="Loading containers: done."
May 16 06:58:23 server1 dockerd[3930]: time="2023-05-16T06:58:23.682671734Z" level=warning msg="WARNING: No swap limit support"
May 16 06:58:23 server1 dockerd[3930]: time="2023-05-16T06:58:23.687758076Z" level=info msg="Docker daemon" commit=9dbdbd4 graphdriver=overlay2 version=23.0.6
May 16 06:58:23 server1 dockerd[3930]: time="2023-05-16T06:58:23.693488362Z" level=info msg="Daemon has completed initialization"
May 16 06:58:23 server1 systemd[1]: Started Docker Application Container Engine.
May 16 06:58:23 server1 dockerd[3930]: time="2023-05-16T06:58:23.975357123Z" level=info msg="API listen on /run/docker.sock"
 ```
