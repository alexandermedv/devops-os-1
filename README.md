# devops-os-1
1. Запускаем в терминале strace /bin/bash -c 'cd /tmp'
В полученном выводе ищем системный вызов, который относится к ls:
   chdir("/tmp")
   
Проверяем нашу догадку, ищем в мануале описание системного вызова chdir:

man 2 chdir

DESCRIPTION
       chdir() changes the current working directory of the calling process to the directory specified in path.

2. Запускаем в терминале strace file
Привлекает внимание строка 
   read(3, "# Locale name alias data base.\n#"..., 4096) = 2996
   
Ищем около нее:
openat(AT_FDCWD, "/etc/magic.mgc", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/magic", O_RDONLY) = 3
Проверяем догадку. Гугл подсказывает, что если есть скомпилированный файл, то информация считывается из /etc/magic.mgc. Если компиляции не существует, используется /etc/magic.

3. 

4. Зомби-процессы не занимают ресурсы в ОС, т.к. это процессы, которые после своего завершения остались в таблице процессов. Но при завершении процесса все ресурсы освобождаются, поэтому такие процессы не тратят ресурсы ОС.
