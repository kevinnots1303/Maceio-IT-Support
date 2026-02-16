import os
import time
import socket

def check_internet(host="8.8.8.8", port=53, timeout=3):
    """Verifica se a conexão com o Google DNS está ativa."""
    try:
        socket.setdefaulttimeout(timeout)
        socket.socket(socket.AF_INET, socket.SOCK_STREAM).connect((host, port))
        return True
    except socket.error:
        return False

def monitor():
    print("--- MONITOR DE REDE KEVIN ADMIN ---")
    print(f"Monitorando conexão para: {socket.gethostname()}")
    
    while True:
        timestamp = time.strftime('%Y-%m-%d %H:%M:%S')
        if check_internet():
            print(f"[{timestamp}] STATUS: ONLINE ✅")
        else:
            print(f"[{timestamp}] STATUS: OFFLINE ❌ - Verifique o Gateway!")
        
        time.sleep(10) # Verifica a cada 10 segundos

if __name__ == "__main__":
    monitor()
