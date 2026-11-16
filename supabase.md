# Supabase - Backend as a Service

## O que e
Alternativa open-source ao Firebase com PostgreSQL.

## Setup

### Criar Projeto
1. Acessar supabase.com
2. Criar novo projeto
3. Anotar URL e anon key

### Instalar Client
npm install @supabase/supabase-js

### Inicializar
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  'YOUR_SUPABASE_URL',
  'YOUR_SUPABASE_ANON_KEY'
)

## Database

### Criar Tabela (SQL Editor)
CREATE TABLE profiles (
  id UUID REFERENCES auth.users PRIMARY KEY,
  username TEXT UNIQUE,
  avatar_url TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE profiles ENABLE ROW LEVEL SECURITY;

-- Policy: users can view all profiles
CREATE POLICY 'Public profiles are viewable by everyone'
  ON profiles FOR SELECT
  USING (true);

-- Policy: users can update own profile
CREATE POLICY 'Users can update own profile'
  ON profiles FOR UPDATE
  USING (auth.uid() = id);

### CRUD Operations

#### Create
const { data, error } = await supabase
  .from('profiles')
  .insert([
    { username: 'john_doe', avatar_url: 'https://example.com/avatar.jpg' }
  ])

#### Read
// All profiles
const { data, error } = await supabase
  .from('profiles')
  .select('*')

// Single profile
const { data, error } = await supabase
  .from('profiles')
  .select('*')
  .eq('username', 'john_doe')
  .single()

// With filters
const { data, error } = await supabase
  .from('profiles')
  .select('*')
  .gt('created_at', '2024-01-01')
  .order('username', { ascending: true })
  .limit(10)

#### Update
const { data, error } = await supabase
  .from('profiles')
  .update({ avatar_url: 'https://example.com/new-avatar.jpg' })
  .eq('username', 'john_doe')

#### Delete
const { error } = await supabase
  .from('profiles')
  .delete()
  .eq('username', 'john_doe')

## Authentication

### Sign Up
const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
})

### Sign In
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password123'
})

### Sign Out
const { error } = await supabase.auth.signOut()

### Get Current User
const { data: { user } } = await supabase.auth.getUser()

### OAuth
const { data, error } = await supabase.auth.signInWithOAuth({
  provider: 'github'
})

## Storage

### Upload File
const { data, error } = await supabase
  .storage
  .from('avatars')
  .upload('avatars/user123.png', file)

### Get Public URL
const { data } = supabase
  .storage
  .from('avatars')
  .getPublicUrl('avatars/user123.png')

### Download File
const { data, error } = await supabase
  .storage
  .from('avatars')
  .download('avatars/user123.png')

### Delete File
const { data, error } = await supabase
  .storage
  .from('avatars')
  .remove(['avatars/user123.png'])

## Realtime

### Subscribe to Changes
const channel = supabase
  .channel('profiles')
  .on('postgres_changes', 
    { event: '*', schema: 'public', table: 'profiles' },
    (payload) => {
      console.log('Change received!', payload)
    }
  )
  .subscribe()

### Unsubscribe
supabase.removeChannel(channel)

## Edge Functions

### Criar Funcao
supabase functions new hello-world

// supabase/functions/hello-world/index.ts
import { serve } from 'https://deno.land/std@0.168.0/http/server.ts'

serve(async (req) => {
  const { name } = await req.json()
  return new Response(JSON.stringify({ message: `Hello ${name}!` }), {
    headers: { 'Content-Type': 'application/json' }
  })
})

### Deploy
supabase functions deploy hello-world

### Chamar Funcao
const { data, error } = await supabase.functions.invoke('hello-world', {
  body: { name: 'World' }
})

## Row Level Security (RLS)

### Exemplos de Policies
-- Users can only see their own data
CREATE POLICY 'Users can view own data'
  ON todos FOR SELECT
  USING (auth.uid() = user_id);

-- Users can only insert their own data
CREATE POLICY 'Users can insert own data'
  ON todos FOR INSERT
  WITH CHECK (auth.uid() = user_id);

-- Admins can see all data
CREATE POLICY 'Admins can view all'
  ON todos FOR SELECT
  USING (auth.jwt() -> 'app_metadata' ->> 'role' = 'admin');

## Best Practices

### Security
- Sempre habilitar RLS
- Usar policies granulares
- Nunca expor service_role key no cliente
- Validar inputs no Edge Functions

### Performance
- Criar indexes apropriados
- Usar pagination
- Evitar N+1 queries
- Cache quando apropriado

### Organizacao
- Usar schemas para organizar tabelas
- Documentar com comments
- Versionar migrations

## Quando Usar
- Prototipos rapidos
- MVPs
- Aplicacoes que precisam de auth + DB + storage
- Times pequenos
- Projetos que precisam de PostgreSQL