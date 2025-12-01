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

