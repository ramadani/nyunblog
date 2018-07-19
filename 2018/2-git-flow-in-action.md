# Git Flow in Action

Inisialisasi git flow di dalam root project.

```bash
$ git flow init

Which branch should be used for bringing forth production releases?
   - master
Branch name for production releases: [master] master
Branch name for "next release" development: [develop] develop

How to name your supporting branch prefixes?
Feature branches? [feature/] feature/
Release branches? [release/] release/
Hotfix branches? [hotfix/] hotfix/
Support branches? [support/] support/
Version tag prefix? [] v
```

Memulai branch baru untuk feature dengan `git flow feature start <name> [<base>]`

```bash
$ git flow feature start login

Switched to a new branch 'feature/login'

...
```

Lalu kita buat contoh code untuk fitur login

```go
func Login(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
	fmt.Fprint(w, "Login Route\n")
}
```

Commit dan push seperti biasa.

```bash
$ git push origin feature/login
```

Lalu engineer lain membuat fitur register

```bash
$ git flow feature start register

Switched to a new branch 'feature/register'

...
```

Dan menambahkan code untuk fitur register

```go
func Register(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
	fmt.Fprint(w, "Register Route\n")
}
```

Lalu engineer B melakukan commit & push

```bash
$ git push origin feature/register
```

Setelah fitur login selesai dan akan di merge ke branch development, jalankan perintah ini:

```bash
$ git flow feature finish login

Switched to branch 'develop'
Updating 9ca703e..d1c026e
Fast-forward
 main.go | 20 ++++++++++++++++++++
 1 file changed, 20 insertions(+)
 create mode 100644 main.go
Deleted branch feature/login (was d1c026e).
```

```bash
$ git flow feature finish register

Switched to branch 'develop'
Updating d1c026e..a90d072
Fast-forward
 main.go | 5 +++++
 1 file changed, 5 insertions(+)
Deleted branch feature/register (was a90d072).
```

Biasanya yang melakukannya adalah lead engineer atau posisi yang bertugas.

Setelah itu push ke branch development:

```bash
$ git push origin develop
```

Setelah itu, persiapan rilis ke production

```bash
$ git flow release start 0.1.0

Switched to a new branch 'release/0.1.0'
...
```

Setelah itu rilis ke branch master

```bash
$ git flow release finish 0.1.0

Deleted branch release/0.1.0 (was a90d072).

Summary of actions:
- Latest objects have been fetched from 'origin'
- Release branch has been merged into 'master'
- The release was tagged 'v0.1.0'
- Release branch has been back-merged into 'develop'
- Release branch 'release/0.1.0' has been deleted
```

Jika butuh hotfix

```bash
$ git flow hotfix start 0.1.1

Switched to a new branch 'hotfix/0.1.1'
```

Lalu hotfix sudah selesai

```bash
$ git flow hotfix finish 0.1.1

Switched to branch 'master'
Your branch is up to date with 'origin/master'.
Merge made by the 'recursive' strategy.
 main.go | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
Switched to branch 'develop'
Merge made by the 'recursive' strategy.
 main.go | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
Deleted branch hotfix/0.1.1 (was 48dff30).

Summary of actions:
- Latest objects have been fetched from 'origin'
- Hotfix branch has been merged into 'master'
- The hotfix was tagged 'v0.1.1'
- Hotfix branch has been back-merged into 'develop'
- Hotfix branch 'hotfix/0.1.1' has been deleted
```
