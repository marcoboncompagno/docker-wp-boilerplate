## Attenzione: lavorare con più siti locali

- Un sito = una cartella progetto separata.
- Ogni compose deve avere un `name` diverso.
- Ogni sito deve usare una porta diversa: `8080`, `8081`, `8082`.
- Ogni sito deve avere il suo `wp-content`.
- Meglio `./wp-content` invece di `../wp-content`.
- Non usare mai `docker compose down -v` se vuoi salvare il DB.
- Non cancellare volumi da Docker Desktop a caso.
- Non dare ai volumi un `name:` fisso condiviso.


# Docker WordPress: backup e restore database

Comandi rapidi per esportare e reimportare il database del progetto Docker WordPress.

## Posizione

Lanciare i comandi dalla cartella dove si trova il file `compose.yaml` / `docker-compose.yml`.

Esempio:

```bash
cd "/Users/marcoboncompagno/Documents/GitHub/adesso trieste/docker-wp-boilerplate"
```

## Backup / export database

Crea un dump del database WordPress nella cartella corrente.

```bash
docker compose exec db mysqldump -uwordpress -pwordpress wordpress > "backup-data.sql"
```

Versione consigliata con data e ora, per non sovrascrivere backup precedenti:

```bash
docker compose exec db mysqldump -uwordpress -pwordpress wordpress > "backup-$(date +%Y-%m-%d_%H-%M-%S).sql"
```

## Restore / import database

Importa un file `.sql` nel database WordPress.

```bash
docker compose exec -T db mysql -uwordpress -pwordpress wordpress < "backup-data.sql"
```

Esempio con file specifico:

```bash
docker compose exec -T db mysql -uwordpress -pwordpress wordpress < "backup-after-media-regenerate-2026-06-28_17-04-50.sql"
```

## Regola da ricordare

```bash
# Export
mysqldump ... > file.sql

# Import
mysql ... < file.sql
```

Nel comando di import è importante usare `-T`.

## Comprimere un backup

```bash
gzip "backup-data.sql"
```

Il file diventa:

```text
backup-data.sql.gz
```

## Decomprimere un backup

```bash
gunzip "backup-data.sql.gz"
```

## Verificare i backup presenti

```bash
ls -lh *.sql
ls -lh *.sql.gz
```

## Credenziali database locali

Queste credenziali sono relative all’ambiente Docker locale.

```text
Database host: db
Database name: wordpress
Database user: wordpress
Database password: wordpress
```


Prima di importare un database, fare sempre un backup del database attuale.
Il restore sovrascrive i dati esistenti nel database di destinazione.



