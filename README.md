# 🧠 ¿Qué significa "scrapear"?
Scrapear una página web es leer su código HTML, extraer el contenido que te interesa (por ejemplo, títulos, texto, enlaces, etc.), y usarlo o guardarlo.

# 🧰 Herramientas que vas a usar
requests – para descargar el HTML.

BeautifulSoup (bs4) – para parsear el HTML y extraer datos.

# 🐍 Paso 1: Instalá las librerías (si no las tenés)
bash
Copiar
Editar
pip install requests beautifulsoup4
# 🧪 Paso 2: Código base para scrapear
python
Copiar
Editar
import requests
from bs4 import BeautifulSoup

# URL objetivo
url = 'https://www.regular-expressions.info/tutorialcnt.html'

# Obtener contenido HTML
response = requests.get(url)
html = response.text

# Parsear HTML con BeautifulSoup
soup = BeautifulSoup(html, 'html.parser')

# Obtener el título de la página
titulo = soup.title.text
print(f"Título: {titulo}")

# Obtener el contenido principal (centrado)
contenido_central = soup.find('td', attrs={'class': 'main'})
if contenido_central:
    print("\nContenido central:")
    print(contenido_central.get_text(strip=True, separator='\n'))
else:
    print("No se encontró contenido central")
🔎 Qué estás haciendo
soup.find(...): buscás una sección específica del HTML (en este caso, un <td> con clase main, que contiene el contenido).

.get_text(...): extraés solo el texto limpio, sin HTML.

💡 Tips prácticos
Podés inspeccionar cualquier página con clic derecho > "Inspeccionar" para ver cómo está estructurado el HTML.

Cada sitio puede tener estructuras diferentes: usás find() o find_all() para navegar el HTML.

📝 ¿Querés guardar el contenido en un archivo?
Podés hacerlo así:

python
Copiar
Editar
with open("contenido.txt", "w", encoding="utf-8") as f:
    f.write(contenido_central.get_text(strip=True, separator='\n'))
🔐 ¿Y si da error o está bloqueado?
Algunos sitios bloquean bots. En ese caso:

Agregás un User-Agent:

python
Copiar
Editar
headers = {'User-Agent': 'Mozilla/5.0'}
response = requests.get(url, headers=headers)
O necesitás usar algo más avanzado como Selenium (para páginas con JavaScript).

✅ ¿Querés probar esto paso a paso?
Te puedo dar versiones para que pegues en VS Code y pruebes por partes.
