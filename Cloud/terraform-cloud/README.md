## Что такое terraform?

[Terraform](https://www.terraform.io/) - это инструмент для создания, изменения и управления инфраструктурой с помощью декларативных конфигурационных файлов. Он позволяет описывать инфраструктуру как код, что упрощает автоматизацию и делает управление ресурсами предсказуемым и повторяемым. Проще говоря, мы пишем код, а затем terraform создает нам кластер.

## Основные команды для запуска кластера и работы с ним:

- `terraform init`
Эта команда инициализирует рабочую директорию Terraform.

- `terraform plan`
Команда terraform plan создает план выполнения, который показывает, какие изменения будут внесены в инфраструктуру.

- `terraform apply`
Команда terraform apply применяет изменения, описанные в файлах конфигурации.

- `terraform destroy`
Команда terraform destroy удаляет все ресурсы, описанные в конфигурации.

### Документация
- https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs
- https://yandex.cloud/en-ru/docs/tutorials/infrastructure-management/terraform-quickstart

Рекомендую использовать сайт terraform, в нём больше подробностей, и в основном в настройке я пользовался именно им.


### Полезные ссылки
- [Примеры конфигов](https://github.com/terraform-yc-modules/terraform-yc-kubernetes)

- [Видео по настройке yandex cloud](https://youtu.be/y1eqR0xL1ZI?si=06fCzdWU0L6vGtZZ)
