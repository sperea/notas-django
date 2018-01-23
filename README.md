# Notas sobre Django

## Despliegue

### Como invocar a gunicorn

Es necesario instalar worker-class gevent. Esto permite arrancar con workers asincrónicos basados en Greenlets (Gevent). Greenlets es una implementación de multihilo cooperativo para Python. Si no, algunas tareas algo lentas pueden dar error de servidor porque Gunicorn considera que éste no responde.

<code>
gunicorn --worker-class gevent --log-level debug --bind 0.0.0.0:8000 Colaboradores.wsgi
</code>

### Cómo configurar nginx

<code>
server {
    server_name {MI IP o MI NOMBRE DE MAQUINA }};

    # Running port
    listen 80;

    access_log off;

    location /static/ {
        alias /<<RUTACOMPLETA>>/static/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header X-Forwarded-Host $server_name;
        proxy_set_header X-Real-IP $remote_addr;
        add_header P3P 'CP="ALL DSP COR PSAa PSDa OUR NOR ONL UNI COM NAV"';
    }
}
</code>
