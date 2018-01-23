# Notas sobre Django

## Despliegue

### Como invocar a gunicorn

Es necesario instalar worker-class gevent. Esto permite arrancar con workers asincrónicos basados en Greenlets (Gevent). Greenlets es una implementación de multihilo cooperativo para Python. Si no, algunas tareas algo lentas pueden dar error de servidor porque Gunicorn considera que éste no responde.

'''bash
gunicorn --worker-class gevent --log-level debug --bind 0.0.0.0:8000 Colaboradores.wsgi
'''
