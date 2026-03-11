Задание 1

Допустимо хранить секретную информацию в файле: personal.auto.tfvars

"result": "sFT8rYlf0byQrqtG"

первая ошибка: блок resource должен содержать обязательно два параметра: тип объекта и уникальное имя в текущем проекте, отсутствует имя.
    вторая ошибка: Terraform не разрешает начинать имя ресурса с цифры.
    третья ошибка: переменная random_string_FAKE не объявлена.

``` 
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"

  ports {
    internal = 80
    external = 9090
  }
}
```
<img width="1204" height="56" alt="изображение" src="https://github.com/user-attachments/assets/bac762ab-556d-47c7-8a38-68ef5fd51693" />


-auto-approve отключает подтверждение изменений через ввод yes
Но с -auto-approve изменения применяются автоматически, что убирает дополнительный контроль изменений.
Ключ полезен для CI/CD pipelines, автоматического развёртывания инфраструктуры и автоматизации

<img width="1087" height="57" alt="изображение" src="https://github.com/user-attachments/assets/7efbf82a-7598-4bbf-9d43-5e825d91db4b" />


{ 
  "version": 4, 
  "terraform_version": "1.14.6", 
  "serial": 8, 
  "lineage": "d6c08d18-58fe-e2e6-7393-047dca8a96bf", 
  "outputs": {}, 
  "resources": [], 
  "check_results": null 
}

Параметр keep_locally = true означает, что Terraform не удаляет образ из локального Docker после destroy.

Из документации Terraform Docker provider для docker_image:
  keep_locally – If true, Terraform will not delete the image from the local Docker daemon after destroy.
