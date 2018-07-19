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

```
func Login(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
	fmt.Fprint(w, "Login Route\n")
}
```

Commit dan push seperti biasa.

```bash
git push origin feature/login
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

Biasanya yang melakukannya adalah lead engineer atau posisi yang bertugas.
