# Anexo de la Práctica 11 — El servidor con pruebas

Código de arranque del anexo de la Práctica 11 de TC2007B.

Es el servidor de Avisos de la Práctica 10 (FastAPI + PostgreSQL + RustFS, todo en
Docker) con sus pruebas de pytest, tal como llegó a la clase de calidad del 6 de
octubre. Una prueba falla: es el primer defecto que vas a corregir.

## Cómo empezar

1. Si tienes otro servidor corriendo (el de la Práctica 10 o el de tu reto), apágalo
   con `docker compose down` en su carpeta: usan los mismos puertos.
2. Copia la configuración y cambia los secretos:

       cp .env.example .env

3. Levanta el servidor y corre las pruebas:

       docker compose up -d --build
       docker compose exec api uv run --no-sync pytest

   Tienes que ver `1 failed, 9 passed, 1 skipped`.
4. Sigue la guía: https://startdroid.com/practicas/anexo-servidor-con-pruebas.html

## Cómo trabajar

`app/` y `tests/` están montadas en el contenedor: guardas un archivo y la siguiente
corrida de pytest ya lo usa, sin reconstruir.

Haz un commit en cada checkpoint de la guía:

    git add -A ; git commit -m "checkpoint a3"

## Uso de IA

Todo commit con código generado por IA debe declararlo con un trailer
`Co-Authored-By`. Ver la política completa en la guía.

## Entrega

Ver la rúbrica en la guía. Sube las ramas y el tag `entrega-pruebas`:
`git push origin --all ; git push origin --tags`.
