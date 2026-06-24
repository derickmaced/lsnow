# L.S Now — Guia de Configuração

## 📁 Estrutura dos arquivos

```
lsnow-premium/
├── index.html          ← Site principal
├── admin/
│   └── index.html      ← Painel admin (gerenciar mensagens)
└── backend/
    ├── server.js       ← Servidor Node.js
    ├── package.json
    ├── .env.example    ← Copie para .env e preencha
    └── messages.json   ← Criado automaticamente ao receber mensagens
```

---

## 🚀 Subindo o Backend

### 1. Instale o Node.js
Baixe em: https://nodejs.org (versão LTS)

### 2. Configure as variáveis de ambiente
```bash
cd backend
cp .env.example .env
```
Edite o arquivo `.env` com seus dados de e-mail e token admin.

### 3. Instale as dependências
```bash
npm install
```

### 4. Inicie o servidor
```bash
# Desenvolvimento
npm run dev

# Produção
npm start
```

O servidor estará disponível em `http://localhost:3001`

---

## 🌐 Configurando o Site

No arquivo `index.html`, altere a linha:
```js
const BACKEND = 'http://localhost:3001';
```
Para a URL do seu servidor de produção:
```js
const BACKEND = 'https://api.seusite.com.br';
```

---

## 📬 Recebendo e-mails (Gmail)

1. Acesse sua conta Google → Segurança → Verificação em 2 etapas → **Senhas de app**
2. Crie uma senha para "Outro aplicativo" com o nome "L.S Now"
3. Cole essa senha em `SMTP_PASS` no arquivo `.env`

---

## 🔐 Painel Admin

Acesse `admin/index.html` no navegador.

Configure:
- **URL do Backend**: `http://localhost:3001` (ou URL de produção)
- **Token de Admin**: o valor de `ADMIN_TOKEN` no `.env`

### Funcionalidades do painel:
- Visualizar todas as mensagens
- Filtrar por lidas/não lidas
- Buscar por nome ou serviço
- Marcar como lida
- Excluir mensagem
- Responder direto pelo WhatsApp
- Exportar todas as mensagens em CSV

---

## 🖼️ Adicionando logos de clientes

No `index.html`, nos cards de cliente, troque:
```html
<div class="client-logo-placeholder">...</div>
```
Por:
```html
<div class="client-logo-img-wrap">
  <img src="nome-da-logo.png" alt="Nome do Cliente">
</div>
```
Coloque o arquivo de imagem (PNG ou SVG) na mesma pasta do `index.html`.

---

## 🎯 Adicionando fotos nos modais de serviço

No JavaScript do `index.html`, localize `const svcData = {...}` e substitua cada slot:
```js
{ model: 'VHD 1220 B', label: 'Câmera Bullet HD' }
```
Adicione a imagem diretamente no HTML da galeria se preferir usar `<img>` real.

---

## 🏭 Deploy em produção

### Opção A — VPS (recomendado)
1. Suba os arquivos do `backend/` para o servidor
2. Use **PM2** para manter o processo ativo:
   ```bash
   npm install -g pm2
   pm2 start server.js --name lsnow
   pm2 save && pm2 startup
   ```
3. Configure **Nginx** como proxy reverso para a porta 3001

### Opção B — Hospedagem compartilhada
O `index.html` funciona sem backend. O formulário fará fallback automático para WhatsApp caso o servidor não esteja disponível.

---

## ✅ Checklist

- [ ] Altere o número de WhatsApp `5511999999999` para o número real
- [ ] Atualize `BACKEND` no `index.html` com a URL do servidor
- [ ] Configure as credenciais SMTP no `.env`
- [ ] Adicione as logos dos clientes reais
- [ ] Adicione as fotos dos modelos nos modais de serviço
- [ ] Substitua o link do Google Reviews no widget flutuante
