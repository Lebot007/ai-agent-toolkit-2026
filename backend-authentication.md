# Backend Authentication - Autenticacao e Autorizacao

## O que e
Sistemas para verificar identidade e controlar acesso.

## Autenticacao vs Autorizacao

### Autenticacao (AuthN)
- Quem e voce?
- Verificar identidade
- Login, senha, tokens

### Autorizacao (AuthZ)
- O que voce pode fazer?
- Controlar acesso
- Permissoes, roles

## Metodos de Autenticacao

### Session-based
app.post('/login', (req, res) => {
  const user = authenticate(req.body.email, req.body.password);
  if (user) {
    req.session.userId = user.id;
    res.json({ success: true });
  } else {
    res.status(401).json({ error: 'Invalid credentials' });
  }
});

### JWT (JSON Web Tokens)
const jwt = require('jsonwebtoken');

// Gerar token
function generateToken(user) {
  return jwt.sign(
    { userId: user.id, email: user.email },
    process.env.JWT_SECRET,
    { expiresIn: '24h' }
  );
}

// Login
app.post('/login', (req, res) => {
  const user = authenticate(req.body.email, req.body.password);
  if (user) {
    const token = generateToken(user);
    res.json({ token });
  } else {
    res.status(401).json({ error: 'Invalid credentials' });
  }
});

// Verificar token
function verifyToken(req, res, next) {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) {
    return res.status(401).json({ error: 'No token provided' });
  }
  
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.userId = decoded.userId;
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
}

## Autorizacao

### Role-Based Access Control (RBAC)
const roles = {
  admin: ['read', 'write', 'delete', 'manage_users'],
  user: ['read', 'write'],
  guest: ['read']
};

function requireRole(role) {
  return (req, res, next) => {
    if (req.user.role === role) {
      next();
    } else {
      res.status(403).json({ error: 'Insufficient permissions' });
    }
  };
}

app.delete('/users/:id', requireAuth, requireRole('admin'), (req, res) => {
  // Delete user
});

## Password Hashing

### bcrypt
const bcrypt = require('bcrypt');

// Hash password
async function hashPassword(password) {
  const salt = await bcrypt.genSalt(10);
  return bcrypt.hash(password, salt);
}

// Verificar password
async function verifyPassword(password, hash) {
  return bcrypt.compare(password, hash);
}

## Refresh Tokens

### Implementacao
function generateRefreshToken(userId) {
  return jwt.sign({ userId }, process.env.REFRESH_SECRET, {
    expiresIn: '7d'
  });
}

// Login retorna access + refresh tokens
app.post('/login', (req, res) => {
  const user = authenticate(req.body);
  const accessToken = generateToken(user);
  const refreshToken = generateRefreshToken(user.id);
  
  // Salvar refresh token no DB
  saveRefreshToken(user.id, refreshToken);
  
  res.json({ accessToken, refreshToken });
});

// Refresh access token
app.post('/refresh', (req, res) => {
  const { refreshToken } = req.body;
  
  try {
    const decoded = jwt.verify(refreshToken, process.env.REFRESH_SECRET);
    if (isValidRefreshToken(decoded.userId, refreshToken)) {
      const newAccessToken = generateToken({ id: decoded.userId });
      res.json({ accessToken: newAccessToken });
    } else {
      res.status(401).json({ error: 'Invalid refresh token' });
    }
  } catch (error) {
    res.status(401).json({ error: 'Invalid refresh token' });
  }
});

## Seguranca

### Best Practices
- Nunca armazenar passwords em plain text
- Usar HTTPS sempre
- Implementar rate limiting
- Validar todos os inputs
- Usar tokens com expiracao
- Implementar logout (invalidar tokens)

### OWASP Top 10
- Broken Authentication
- Sensitive Data Exposure
- Security Misconfiguration

## Frameworks

### Node.js
- Passport.js
- jsonwebtoken
- bcrypt

### Python
- Flask-Login
- Django Auth
- FastAPI Users

### Java
- Spring Security
- Apache Shiro

## Quando Usar
- Qualquer aplicacao com usuarios
- APIs que precisam de autenticacao
- Sistemas com diferentes niveis de acesso
- Protecao de dados sensiveis
