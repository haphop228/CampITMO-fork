## Что такое terraform?

Файлы для [terraform](https://www.terraform.io/) для автоматического создания [пользователей с методом аутентификации `userpass`](https://developer.hashicorp.com/vault/docs/auth) и создания [политик](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-policies), ограничивающих доступ этих пользователей к заданным ресурсам в [`kv engine`](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-secrets-engines).

## Основные команды для запуска кластера и работы с ним:
-`terraform init`
Эта команда инициализирует рабочую директорию Terraform.
-`terraform plan`
Команда terraform plan создает план выполнения, который показывает, какие изменения будут внесены в инфраструктуру.
-`terraform apply`
Команда terraform apply применяет изменения, описанные в файлах конфигурации.
-`terraform destroy`
Команда terraform destroy удаляет все ресурсы, описанные в конфигурации.

### Prerequesties

- `docker`
- `terraform`

### Команды для запуска

1. `docker run -d -p 8200:8200 hashicorp/vault server -dev` -- запускается `vault` в `dev` режиме.
2. `terraform apply -auto-aprove -var-file vars.tfvars` -- создаются политики и пользователи с помощью `terraform`.

После выполнения пункта `1` можно зайти на [http://localhost:8200/](http://localhost:8200/) и потыкать в UI `vault`.

## Запустить на кластере в облаке

0. подключиться к кластеру в облаку и заполнить файл `vars.tfvars`
1. `kubectl port-forward svc/vault 8200:8200 -n vault`
2. `terraform init`
3. `terraform apply -var-file vars.tfvars`

### Как откатить изменения?

`terraform destroy -var-file vars.tfvars`
