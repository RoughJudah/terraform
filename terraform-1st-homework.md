Задание 1

Допустимо хранить секретную информацию в файле: personal.auto.tfvars

"result": "A7m4K9q2T8b1R5x6"

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
<img width="1012" height="62" alt="изображение" src="https://github.com/user-attachments/assets/c8eb7f7c-4341-4d90-be67-cacdc8c00ee1" />

-auto-approve отключает подтверждение изменений через ввод yes
Но с -auto-approve изменения применяются автоматически, что убирает дополнительный контроль изменений.
Ключ полезен для CI/CD pipelines, автоматического развёртывания инфраструктуры и автоматизации

<img width="978" height="68" alt="изображение" src="https://github.com/user-attachments/assets/a6d54c16-b338-4e7a-8498-1fdcf3d37eac" />

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
