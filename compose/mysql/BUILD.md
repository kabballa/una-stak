Iată cum poți modifica fișierul `docker-compose.yml` pentru a muta parolele din variabile de mediu în Docker Secrets:

### 1. **Creează secretele folosind Docker Secrets**

```bash
echo "my_root_password" | docker secret create mysql_root_password -
echo "my_password" | docker secret create mysql_password -
```


### Explicații:

- **Secretele**: Folosim secretele `mysql_root_password`, `mysql_user`, `mysql_password` și `mysql_database`, montate ca fișiere în `/run/secrets/`.
- **Command pentru MySQL**: În secțiunea `command`, se folosesc `cat` pentru a citi parolele și alte informații din fișierele de secrete și a le exporta ca variabile de mediu.
- **phpMyAdmin**: `PMA_PASSWORD_FILE` se folosește pentru a citi parola root din secret, în loc să fie direct în fișierul `.env`.

Acum toate parolele sunt stocate în secrete Docker, iar variabilele de mediu sensibile nu vor mai fi expuse direct în fișiere sau imagini.