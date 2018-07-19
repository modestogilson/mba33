## Comandos Git

Segue abaixo uma sessão que muda o master e publica de volta no Github.

- de início faz pull do github para se sincronizar com a última versão
- verifica que há um branch local antigo e deleta
- cria um novo branch de mudança, note que o branch mudou de master para motta
- editei o arquivo do profile, fazendo as alterações
- voltei ao bash e fiz commit das mudanças
- mudei para o branch master no repo local
- fiz o merge das alterações do branch motta no master local
- fiz push do master para o github

![Merge](https://i.imgur.com/pVKZH8X.png)

Caso haja conflito, ver abaixo, tente sincronizar com master novamente, pois alguém pode ter aceitado um pull request e modificado o master.

![](https://i.imgur.com/mgzzRKu.png)

Outro exemplo, incluindo vários arquivos:

	$ git status
	On branch master
	Your branch is up to date with 'origin/master'.
	
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	
	        demo/
	        refs/story-02-microservice.pdf
	        refs/story-02-uml.pdf
	        refs/story-03-container.pdf
	
	nothing added to commit but untracked files present (use "git add" to track)

	$ git pull
	remote: Counting objects: 10, done.
	remote: Compressing objects: 100% (7/7), done.
	remote: Total 10 (delta 3), reused 9 (delta 3), pack-reused 0
	Unpacking objects: 100% (10/10), done.
	From github.com:bamplifier/mba33
	   8ad3560..ea63461  master     -> origin/master
	Updating 8ad3560..ea63461
	Fast-forward
	 README.md | 16 +++++++++++++++-
	 1 file changed, 15 insertions(+), 1 deletion(-)
	
	$ git branch
	* master
	  motta
	
	$ git branch -D motta
	Deleted branch motta (was ad10d46).
	
	$ git checkout -b motta
	Switched to a new branch 'motta'
	
	$ git status
	On branch motta
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	
	        demo/
	        refs/story-02-microservice.pdf
	        refs/story-02-uml.pdf
	        refs/story-03-container.pdf
	
	nothing added to commit but untracked files present (use "git add" to track)
	
	$ git add . -A
	
	$ git commit -am "add uml, microservice e container"
	[motta 9a70b81] add uml, microservice e container
	 6 files changed, 46 insertions(+)
	 create mode 100644 demo/docker-py/Dockerfile
	 create mode 100644 demo/docker-py/app.py
	 create mode 100644 demo/docker-py/requirements.txt
	 create mode 100644 refs/story-02-microservice.pdf
	 create mode 100644 refs/story-02-uml.pdf
	 create mode 100644 refs/story-03-container.pdf
	
	$ git checkout master
	Switched to branch 'master'
	Your branch is up to date with 'origin/master'.
	
	$ git merge --no-ff motta
	Merge made by the 'recursive' strategy.
	 demo/docker-py/Dockerfile       |  20 ++++++++++++++++++++
	 demo/docker-py/app.py           |  24 ++++++++++++++++++++++++
	 demo/docker-py/requirements.txt |   2 ++
	 refs/story-02-microservice.pdf  | Bin 0 -> 2117454 bytes
	 refs/story-02-uml.pdf           | Bin 0 -> 701873 bytes
	 refs/story-03-container.pdf     | Bin 0 -> 1163836 bytes
	 6 files changed, 46 insertions(+)
	 create mode 100644 demo/docker-py/Dockerfile
	 create mode 100644 demo/docker-py/app.py
	 create mode 100644 demo/docker-py/requirements.txt
	 create mode 100644 refs/story-02-microservice.pdf
	 create mode 100644 refs/story-02-uml.pdf
	 create mode 100644 refs/story-03-container.pdf
	
	$ git push origin master
	Enumerating objects: 14, done.
	Counting objects: 100% (14/14), done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (10/10), done.
	Writing objects: 100% (12/12), 3.33 MiB | 585.00 KiB/s, done.
	Total 12 (delta 2), reused 0 (delta 0)
	remote: Resolving deltas: 100% (2/2), completed with 1 local object.
	To github.com:bamplifier/mba33.git
	   ea63461..82aa3d8  master -> master
	
	$ git status
	On branch master
	Your branch is up to date with 'origin/master'.
	
	nothing to commit, working tree clean
