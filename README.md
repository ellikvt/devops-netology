# devops-netology

Created by: Tormyshev Vadim / Тормышев Вадим

Домашнее задание к занятию «2.1. Системы контроля версий.»
----------------------------------------------------------
----------------------------------------------------------

Tue Oct 26 07:51:41 UTC 2021 | I have modified the file  
Tue Oct 26 07:58:30 UTC 2021 | I have modified the file after "git add" command was implemented to it  
Tue Oct 26 21:14:49 UTC 2021 | I have modified the file after "git restore --staged README.md" was implemented to it  

После создания каталога terraform и добавления в него файла
 .gitignore, содержащего описания правил игнорирования, будут проигнорированы
 файлы, указанные ниже: 

каждый путь, который будет начинаться внутри каталога terraform и будет иметь
имя каталога ".terraform" в конце и любые типы/количество файлов в каталоге ".terraform"

файл ./terraform/crash.log 

все файлы каталога terraform, которые будут иметь расширение "tfvars"

файлы override.tf, override.tf.json в каталоге terraform
файлы в каталоге terraform, имена которых заканчиваются последовательностями символов
'_override.tf', '_override.tf.json'

файлы '.terraformrc', 'terraform.rc' в каталоге terraform

Домашнее задание к занятию «2.2. Основы Git.»
----------------------------------------------------------
----------------------------------------------------------
    
github: https://github.com/ellikvt/devops-netology.git
  
gitlab: https://gitlab.com/ellikvt/devops-netology.git
  
bitbucket: https://ellikvt@bitbucket.org/ellikvt/netology.git
  
  
Домашнее задание к занятию «2.3. Ветвления в Git.»
----------------------------------------------------------
----------------------------------------------------------

  

Выполненное задание - в репозитории: https://github.com/ellikvt/devops-netology.git

В тексте задания допущена ошибка:
```bash
#!/bin/bash
# display command line options
count=1
for param in "$@"; do
<<<<<<< HEAD
    echo "\$@ Parameter #$count = $param"
=======
    echo "Parameter: $param"
>>>>>>> dc4688f... git 2.3 rebase @ instead *
    count=$(( $count + 1 ))
done
```
Удалим метки, отдав предпочтение варианту
```bash
echo "\$@ Parameter #$count = $param"
```
  
Если решить конфликт таким образом, то после rebase получим состояние:
![Два мержа](02-git-03-branching/img/01.png)
  
Продолжая решать задание буквально и выполнив git merge git-rebase, получим состояние:
![Сложная история после последнего мержа](02-git-03-branching/img/02.png)
  
Если же разрешить конфликт при rebase, отдав предпочтение варианту:
```bash
echo "Parameter: $param"
```
то вычисляемая Гитом разница для выполнения rebase будет простой, так как будет выбран
вариант разрешения конфликта из более нового файла rebase из ветки git-rebase
  
При использовании `echo "\$@ Parameter #$count = $param"` для рарешения конфликта
Гиту приходится брать последнюю версию rebase.sh из main, которая старее rebase.sh 
из ветки git-rebase, коммит более старой версии находится к тому же перед коммитом первого 
мержа. Как последствия этого, Гит вычисляет разницу, используя два коммита из main 
, один из них - мерж коммит, также он "тянет" старые изменения и создает новые два коммита
на разных ветках (git-rebase and main) вместо одного коммита в main.
Затем попытка выполнить последний мерж уже происходит естественно рекурсивно и самое главное, 
что она также бесконфликтна и выполняется автоматически (применением) более новых изменений
в файлах rebase.sh и merge.sh. В результате в ветке main получим merge.sh с изменениями
не соответствующими его версии из первого мержа.
  
  
Домашнее задание к занятию «2.4. Инструменты Git»
----------------------------------------------------------
----------------------------------------------------------
  
1. hash=aefead2207ef7e2aa5dc81a34aedf0cad4c32545, получен командой
`git log | grep aefea`
Notes / Комментарии коммита:
```bash
diff --git a/CHANGELOG.md b/CHANGELOG.md
index 86d70e3e0..588d807b1 100644
--- a/CHANGELOG.md
+++ b/CHANGELOG.md
@@ -27,6 +27,7 @@ BUG FIXES:
 * backend/s3: Prefer AWS shared configuration over EC2 metadata credentials by default ([#25134](https://github.com/hashicorp/terraform/issues/25134))
 * backend/s3: Prefer ECS credentials over EC2 metadata credentials by default ([#25134](https://github.com/hashicorp/terraform/issues/25134))
 * backend/s3: Remove hardcoded AWS Provider messaging ([#25134](https://github.com/hashicorp/terraform/issues/25134))
+* command: Fix bug with global `-v`/`-version`/`--version` flags introduced in 0.13.0beta2 [GH-25277]
 * command/0.13upgrade: Fix `0.13upgrade` usage help text to include options ([#25127](https://github.com/hashicorp/terraform/issues/25127))
 * command/0.13upgrade: Do not add source for builtin provider ([#25215](https://github.com/hashicorp/terraform/issues/25215))
 * command/apply: Fix bug which caused Terraform to silently exit on Windows when using absolute plan path ([#25233](https://github.com/hashicorp/terraform/issues/25233))
```
Получены командой: git show aefead2207ef7e2aa5dc81a34aedf0cad4c32545 --pretty=format:'%N'
  
commit message: `Update CHANGELOG.md`
Получено командой git show aefead2207ef7e2aa5dc81a34aedf0cad4c32545
  
2. Ответ : `tag: v0.12.23`
   Получен командой: `git show 85024d3`
  
3. Ответ : 2 родителя ( 9ea88f22f и 56cd7859e )
   Можно получить при помощи: 
   ```bash
   git checkout b8d720
   git log --pretty=format:'%h %S' --graph
   ```
   И в дереве коммитов видно наглядно..
   А можно получить при помощи:
   `git show b8d720`, и в сообщении коммита есть ссылки на его родителей (их хэши) 
   а также информация, что это - мерж коммит.
   
4. Ответ:
```bash
commit 33ff1c03bb960b332be3af2e333462dde88b279e
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 19 15:04:05 2020 +0000

    v0.12.24

commit b14b74c4939dcab573326f4e3ee2a62e23e12f89
Author: Chris Griggs <cgriggs@hashicorp.com>
Date:   Tue Mar 10 08:59:20 2020 -0700

    [Website] vmc provider links

commit 3f235065b9347a758efadc92295b540ee0a5e26e
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Mar 19 10:39:31 2020 -0400

    Update CHANGELOG.md

commit 6ae64e247b332925b872447e9ce869657281c2bf
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Mar 19 10:20:10 2020 -0400

    registry: Fix panic when server is unreachable
    
    Non-HTTP errors previously resulted in a panic due to dereferencing the
    resp pointer while it was nil, as part of rendering the error message.
    This commit changes the error message formatting to cope with a nil
    response, and extends test coverage.
    
    Fixes #24384

commit 5c619ca1baf2e21a155fcdb4c264cc9e24a2a353
Author: Nick Fagerlund <nick.fagerlund@gmail.com>
Date:   Wed Mar 18 12:30:20 2020 -0700

    website: Remove links to the getting started guide's old location
    
    Since these links were in the soon-to-be-deprecated 0.11 language section, I
    think we can just remove them without needing to find an equivalent link.

commit 06275647e2b53d97d4f0a19a0fec11f6d69820b5
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Wed Mar 18 10:57:06 2020 -0400

    Update CHANGELOG.md

commit d5f9411f5108260320064349b757f55c09bc4b80
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Tue Mar 17 13:21:35 2020 -0400

    command: Fix bug when using terraform login on Windows

commit 4b6d06cc5dcb78af637bbb19c198faff37a066ed
Author: Pam Selle <pam@hashicorp.com>
Date:   Tue Mar 10 12:04:50 2020 -0400

    Update CHANGELOG.md

commit dd01a35078f040ca984cdd349f18d0b67e486c35
Author: Kristin Laemmert <mildwonkey@users.noreply.github.com>
Date:   Thu Mar 5 16:32:43 2020 -0500

    Update CHANGELOG.md

commit 225466bc3e5f35baa5d07197bbc079345b77525e
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 21:12:06 2020 +0000

    Cleanup after v0.12.23 release

commit 85024d3100126de36331c6982bfaac02cdab9e76
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 20:56:10 2020 +0000

    v0.12.23
```
Получен командой : `git log v0.12.23~..v0.12.24`. Но для начала выполнена команда:
```bash
git log v0.12.23~..v0.12.24 --oneline
    
33ff1c03b v0.12.24
b14b74c49 [Website] vmc provider links
3f235065b Update CHANGELOG.md
6ae64e247 registry: Fix panic when server is unreachable
5c619ca1b website: Remove links to the getting started guide's old location
06275647e Update CHANGELOG.md
d5f9411f5 command: Fix bug when using terraform login on Windows
4b6d06cc5 Update CHANGELOG.md
dd01a3507 Update CHANGELOG.md
225466bc3 Cleanup after v0.12.23 release
85024d310 v0.12.23
```
Для понимания объема, содержания, наглядности.
  
5. Команда `git grep -p 'func providerSource'` выдаст имена файлов и функции, 
   где присутствует совпадение   В данном случае совпадений немного и все они 
   в файле с одним и тем же именем provider_source.go.
   Теперь, применив `git log -L :'func providerSource':provider_source.go`, 
   получим в выводе три коммита, в которых func providerSource описывалась. 
   Видно, что она впервые появилась в 8c928e83589d90a031f811fae52a81be7153e82f,
   затем разработчик дописал ее тело, указав оператор возврата из функции return 
   и откорректировав комментарии в ее теле. В коммите 
   5af1e6234ab6da412fb8637393c5a17a1b293663 функция окончательно отредактирована.
  
6. Выведем результат выполнения `git grep -c -p globalPluginDirs`:
```bash
commands.go:2
internal/command/cliconfig/config_unix.go:1
plugins.go:2
```
   Итого: 5 коммитов. Используем имена файлов для поиска всех коммитов, где 
   globalPluginDirs менялась:
```bash
 git log -L:globalPluginDirs:plugins.go && git log -L:globalPluginDirs:internal/command/cliconfig/config_unix.go && git log -L:globalPluginDirs:commands.go
```
  и получим эти 5 коммитов:
  78b12205587fe839f10d946ea3fdc06719decb05  
  52dbf94834cb970b510f2fba853a5b49ad9b1a46  
  41ab0aef7a0fe030e84018973a64135b11abcd70  
  66ebff90cdfaa6938f26f908c7ebad8d547fea17  
  8364383c359a6b738a436d1b7745ccdce178df47  
  
7. Используем git log: 
```bash
git log -S synchronizedWriters --oneline --pretty=format:'%h %s %ad'
bdfea50cc remove unused Mon Nov 30 18:02:04 2020 -0500
fd4f7eb0b remove prefixed io Wed Oct 21 13:06:23 2020 -0400
5ac311e2a main: synchronize writes to VT100-faker on Windows Wed May 3 16:25:41 2017 -0700
```
  
Таким образом работа с кодом функции была в 3 коммитах.
Затем посмотрим в каких коммитах и каким образом функция редактировалась:
```bash
git show bdfea50cc | grep synchronizedWriters && echo '---' && git show fd4f7eb0b | grep synchronizedWriters && echo '---' && git show 5ac311e2a | grep synchronizedWriters

-// synchronizedWriters takes a set of writers and returns wrappers that ensure
-func synchronizedWriters(targets ...io.Writer) []io.Writer {
---
-               wrapped := synchronizedWriters(stdout, stderr)
---
+               wrapped := synchronizedWriters(stdout, stderr)
+// synchronizedWriters takes a set of writers and returns wrappers that ensure
+func synchronizedWriters(targets ...io.Writer) []io.Writer {
```
Видим, что она добавлена впервые в коммит 5ac311e2a.
Теперь если попробуем использовать: `git blame synchronizedWriters` то мы не получим никакого
результата, даже используя ключи -С или -М. Вообще анализируя все три коммита найденные ранее,
можно сразу видеть странное наличие функции synchronizedWriters в коде. К тому же она была
в конце концов удалена как неиспользуемая, судя по `bdfea50cc remove unused Mon Nov 30 18:02:04 2020 -0500`.
Если почитать документацию по git blame, git log, то в man git blame есть рекомендация - 
использовать git log --diff-filter в случаях, когда строки в искомых файлах были что называется сделаны простой копи-пастой из уже сушествующих файлов. Иногда это бывает из-за небрежности разработчика и плохого
рефакторинга кода:
```bash
git log --diff-filter=A --pretty=short -- synchronized_writers.go

commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
Author: Martin Atkins <mart@degeneration.co.uk>
  
 main: synchronize writes to VT100-faker on Windows
```
  
выполнив `git show 5ac311e2a --pretty=format: '%an %cn', получим:
```bash

Martin Atkins Martin Atkins
diff --git a/main.go b/main.go
index b94de2ebc..237581200 100644
--- a/main.go
+++ b/main.go
@@ -258,6 +258,15 @@ func copyOutput(r io.Reader, doneCh chan<- struct{}) {
 	if runtime.GOOS == "windows" {
 		stdout = colorable.NewColorableStdout()
 		stderr = colorable.NewColorableStderr()
+
+		// colorable is not concurrency-safe when stdout and stderr are the
+		// same console, so we need to add some synchronization to ensure that
+		// we can't be concurrently writing to both stderr and stdout at
+		// once, or else we get intermingled writes that create gibberish
+		// in the console.
+		wrapped := synchronizedWriters(stdout, stderr)
+		stdout = wrapped[0]
+		stderr = wrapped[1]
 	}
 
 	var wg sync.WaitGroup
diff --git a/synchronized_writers.go b/synchronized_writers.go
new file mode 100644
index 000000000..2533d1316
--- /dev/null
+++ b/synchronized_writers.go
@@ -0,0 +1,31 @@
+package main
+
+import (
+	"io"
+	"sync"
+)
+
+type synchronizedWriter struct {
+	io.Writer
+	mutex *sync.Mutex
+}
+
+// synchronizedWriters takes a set of writers and returns wrappers that ensure
+// that only one write can be outstanding at a time across the whole set.
+func synchronizedWriters(targets ...io.Writer) []io.Writer {
+	mutex := &sync.Mutex{}
+	ret := make([]io.Writer, len(targets))
+	for i, target := range targets {
+		ret[i] = &synchronizedWriter{
+			Writer: target,
+			mutex:  mutex,
+		}
+	}
+	return ret
+}
+
+func (w *synchronizedWriter) Write(p []byte) (int, error) {
+	w.mutex.Lock()
+	defer w.mutex.Unlock()
+	return w.Writer.Write(p)
+}
```
таким образом здесь можно адресовать свои вопросы только товарищу Martin Atkins.


