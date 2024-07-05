## Что такое terraform?

[terraform](https://www.terraform.io/) для автоматического создания [пользователей с методом аутентификации `userpass`](https://developer.hashicorp.com/vault/docs/auth) и создания [политик](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-policies), ограничивающих доступ этих пользователей к заданным ресурсам в [`kv engine`](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-secrets-engines).

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

### Пример готовых конфигураций на yandex cloud
https://github.com/terraform-yc-modules/terraform-yc-kubernetes

Оглавление
Что такое Terraform?
Установка Terraform
Основные команды Terraform
Пример конфигурационного файла
Инициализация и применение конфигурации
Заключение
Что такое Terraform?
Terraform - это инструмент для создания, изменения и управления инфраструктурой с помощью декларативных конфигурационных файлов. Он позволяет описывать инфраструктуру как код, что упрощает автоматизацию и делает управление ресурсами предсказуемым и повторяемым.

Установка Terraform
Для установки Terraform следуйте этим шагам:

Перейдите на страницу загрузки Terraform.
Скачайте архив с Terraform для вашей операционной системы.
Разархивируйте скачанный файл и поместите исполняемый файл terraform в папку, указанную в переменной окружения PATH.
Чтобы убедиться, что Terraform установлен правильно, выполните команду:

sh
Копировать код
terraform --version
Основные команды Terraform
terraform init: Инициализирует рабочую директорию, загружает необходимые провайдеры и модули.
terraform plan: Создает план выполнения, показывая, какие изменения будут внесены в инфраструктуру.
terraform apply: Применяет изменения, создавая, изменяя или удаляя ресурсы в соответствии с конфигурацией.
terraform destroy: Удаляет все ресурсы, описанные в конфигурации.
Пример конфигурационного файла
Ниже приведен пример конфигурационного файла Terraform, который создает виртуальную машину (VM) в Yandex Cloud:

hcl
Копировать код
# Определяем провайдера Yandex Cloud
provider "yandex" {
  cloud_id  = var.cloud_id
  folder_id = var.folder_id
  zone      = var.zone
  service_account_key_file = file("path/to/key.json")
}

# Определяем виртуальную машину
resource "yandex_compute_instance" "my_vm" {
  name        = "example-vm"
  platform_id = "standard-v2"
  zone        = var.zone

  resources {
    cores  = 2
    memory = 4
  }

  boot_disk {
    initialize_params {
      image_id = "fd8q8j1hb2q9vksrjrki"
    }
  }

  network_interface {
    subnet_id = yandex_vpc_subnet.my_subnet.id
    nat       = true
  }

  metadata = {
    ssh-keys = "ubuntu:${file("~/.ssh/id_rsa.pub")}"
  }
}

# Определяем сеть
resource "yandex_vpc_network" "my_network" {
  name = "example-network"
}

# Определяем подсеть
resource "yandex_vpc_subnet" "my_subnet" {
  name           = "example-subnet"
  zone           = var.zone
  network_id     = yandex_vpc_network.my_network.id
  v4_cidr_blocks = ["10.0.0.0/24"]
}
Инициализация и применение конфигурации
Инициализация:
Откройте терминал в директории с вашим файлом конфигурации и выполните команду:

sh
Копировать код
terraform init
Создание плана:
После инициализации выполните команду:

sh
Копировать код
terraform plan
Применение конфигурации:
Если все в порядке, примените конфигурацию с помощью команды:

sh
Копировать код
terraform apply
Удаление ресурсов:
Когда ресурсы больше не нужны, вы можете удалить их с помощью команды:

sh
Копировать код
terraform destroy

