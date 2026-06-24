FROM python:3.11-slim  
# Criando usuário não-root (segurança) 
RUN useradd --create-home --shell /bin/bash appuser

# Definindo diretório de trabalho 
WORKDIR /app 
 
# Copiando requirements primeiro (cache do Docker)   
COPY app/requirements.txt .

# Instalando dependências   
RUN pip install --no-cache-dir -r requirements.txt 
 
# Copiando código da aplicação   
COPY app/ .

# Mudando para usuário não-root   
USER appuser 
 
# Expondo porta (configurável via variável)   
EXPOSE ${PORT:-5000} 
 
# Comando de inicialização   
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "2", "app:app"]
