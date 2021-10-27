# devops-netology
Tue Oct 26 07:51:41 UTC 2021 | I have modified the file
Tue Oct 26 07:58:30 UTC 2021 | I have modified the file after "git add" command was implemented to it
Tue Oct 26 21:14:49 UTC 2021 | I have modified the file after "git restore --staged README.md" was implemented to it

После добавления ./terraform/.gitignore файлы, указанные ниже, будут проигнорированы:

каждый путь, который будет начинаться с этого каталога и будет иметь
имя каталога ".terraform" в конце и любые типы/количество файлов в каталоге ".terraform"

файл ./terraform/crash.log

все файлы каталога terraform, которые будут иметь расширение "tfvars"

файлы override.tf, override.tf.json в каталоге terraform
файлы в каталоге terraform, имена которых заканчиваются последовательностями символов
'_override.tf', '_override.tf.json'

файлы '.terraformrc', 'terraform.rc' в каталоге terraform
