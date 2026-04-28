# AT WordPress Docker Environment

Ambiente Docker locale per sviluppare un sito WordPress con `wp-content` montato dal filesystem locale.

Il progetto usa:

- WordPress latest
- MariaDB 10.6
- Docker Compose
- "wp-content" montato come volume locale

## Struttura del progetto

```text
AT/
├─ wp-docker/
│  └─ compose.yaml
└─ wp-content/
   ├─ themes/
   │  └─ your-theme-here/
   ├─ plugins/
   └─ uploads/