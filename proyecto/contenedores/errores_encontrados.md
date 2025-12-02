## Errores Encontrados en la Configuración de Contenedores

---

### 🟥 Error 1 — Nginx NO expone métricas
El job en *prometheus.yml* apuntaba a **nginx:9113**.  
Nginx Alpine no incluye un exporter por defecto.  

**Resultado:** Target en estado **DOWN**.

**Solución aplicada:**  
✔️ Comenté el job de nginx en prometheus.yml

---

### 🟥 Error 2 — Tiempo de espera del Compose
Apareció el siguiente error:  
**Error response from daemon: timeout on HTTP request**

**Solución:**  
✔️ Ejecuté: export COMPOSE_HTTP_TIMEOUT=200

---

### 🟥 Error 3 — Directorios mal montados o permisos
Prometheus mostraba errores como:  
**Error loading config: couldn't read file ...**

**Solución:**  
✔️ Revisé rutas de montajes  
✔️ Corregí permisos y reinicié los contenedores

---

### 🟥 Error 4 — Targets DOWN
En la interfaz de Prometheus aparecía:  
**nginx:9113 — DOWN**

**Solución aplicada:**  
✔️ Comenté el job de nginx  
✔️ Reinicié Prometheus  
✔️ Verifiqué en: http://192.168.100.116:9090/targets

---


===== Contenido de error_config.txt =====
yaml.scanner.ScannerError: while scanning a simple key
  in "./docker-compose.yml", line 48, column 1
could not find expected ':'
  in "./docker-compose.yml", line 49, column 1

===== Contenido de primer_error.txt =====
yaml.scanner.ScannerError: while scanning a simple key
  in "./docker-compose.yml", line 48, column 1
could not find expected ':'
  in "./docker-compose.yml", line 49, column 1
## Errores encontrados en docker-compose.yml

### Error — Redes inconsistentes (monitoring-network)
Problema: El servicio Redis usaba la red 'monitoring-network', pero dicha red no existía.  
Solución: Cambié 'monitoring-network' por 'monitoring'.

---

### Error — Indentación rota y texto incrustado en Prometheus
Problema: El bloque de Prometheus tenía texto incrustado dentro del YAML, rompiendo la sintaxis.  
Solución: Eliminé el texto y corregí la indentación final del bloque.

---

### Error — Loki sin archivo de configuración
Problema: Loki usaba el archivo '/etc/loki/local-config.yaml' que no existía en la VM.  
Solución: Creé un archivo local-config.yaml y lo monté correctamente.
---

### Error — Volumen incorrecto en Grafana
Problema: En Grafana se usaba el volumen 'grafana-data' pero al final del archivo YAML solo estaba declarado 'grafana-storage'.  
Solución: Agregué la declaración correcta del volumen 'grafana-data'.

---

### Error — Indentación incorrecta en varios servicios
Problema: Los servicios tenían claves sin indentación correcta (ports, environment, volumes, etc.).  
Solución: Reparé toda la indentación del archivo YAML.

---

### Error — Comentarios y texto mezclado dentro del YAML
Problema: Había comentarios largos incrustados dentro del YAML, lo cual rompe la estructura del archivo.  
Solución: Eliminé el texto y lo dejé fuera del .yml para permitir que Docker Compose lo procese correctamente.


