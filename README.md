### Демонстрационный стенд pacemaker c virtualbox fence

  Данный vagrant-стенд развёртывает 3 виртуальных машины с использованием провайдера virtualbox.
Внутри виртуальных машин с помощью ansible развёртывается чистый pacemaker-кластер с настроенным фенсингом virtualbox.

  Фенсинг virtualbox требует доступа по ssh на машину-гипервизор с использованием логина и пароля. Права пользователя должны быть достаточными для использования на гипервизоре консольных утилит virtualbox (VBoxManage, etc.)

##### Используемые инструменты:
  - Virtualbox + Vagrant
  - Pacemaker + Corosync
  - ClusterLabs fence agents

##### Порядок запуска:
```
git clone <this repo>
vagrant up
ansible-playbook main.yml
```

##### Комментарии:
  Для корректной работы фенсинга нужно указать адрес машины-гипервизора и учетные данные для доступа на неё по ssh в файле [hosts.yml](hosts.yml). По-умолчанию подразумевается, что адрес гипервизора 192.168.11.1, логин - mbfx, пароль - strong_pass.

  Проверить доступность управления виртуальными машинами с нод кластера можно выполнив на нодах команды:
```
fence_vbox --ip="192.168.11.1" --username="mbfx" --password=strong_pass --ssh --plug="pcs1" -v
fence_vbox --ip="192.168.11.1" --username="mbfx" --password=strong_pass --ssh --plug="pcs1" -o status
```
  Они должны вернуть информацию о виртуальных машинах.
