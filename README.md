# 🎵 Sistema Musical — Gerenciador de Artistas e Músicas

Um sistema web completo desenvolvido em **PHP** e **MySQL** para gerenciamento de artistas, acervo musical e playlists integradas ao YouTube. O projeto conta com autenticação de usuários, controle de sessão, operações de **CRUD** completo, upload e redimensionamento automático de imagens, além de busca e filtros dinâmicos na biblioteca musical.

## 🚀 Funcionalidades

* **🔐 Autenticação & Segurança:**
  * Login seguro utilizando senhas criptografadas com hash **bcrypt** (`password_hash` / `password_verify`).
  * Proteção de páginas por controle de sessão PHP (`valida_sessao.php`).
  * Proteção contra **SQL Injection** através do uso sistemático de *Prepared Statements*.
  * Higienização de dados contra **XSS** (`htmlspecialchars`).

* **🎤 Gerenciamento de Artistas (CRUD):**
  * Cadastro, listagem, edição e exclusão de artistas.
  * Upload de foto do artista com validação de formato/tamanho e redimensionamento automático (função usando a biblioteca GD).
  * Regra de integridade referencial: impede a exclusão de artistas que possuam músicas vinculadas.

* **🎵 Gerenciamento de Músicas (CRUD):**
  * Vínculo direto de cada música a um artista (chave estrangeira `artista_id`).
  * Suporte a dados detalhados: título, álbum, gênero, letra e capa do álbum.
  * Validação e extração dinâmica do ID do vídeo a partir de URLs do **YouTube** (`watch`, `youtu.be`, `embed`).
  * Remoção automática dos arquivos de imagem do servidor ao excluir uma música (`unlink`).

* **🎼 Biblioteca Musical Dinâmica:**
  * Listagem completa de todas as músicas cadastradas no sistema com `JOIN` de tabelas.
  * Filtros combináveis e simultâneos por **busca geral** (título, álbum ou artista), **artista específico** e **gênero**.
  * Manutenção dos parâmetros de filtro na URL durante ações na página.
  * Redirecionamento direto para o reprodutor do YouTube (`target="_blank"` com `rel="noopener noreferrer"` para segurança).

## 🛠️ Tecnologias Utilizadas

* **Linguagem Server-Side:** PHP 8.x
* **Banco de Dados:** MySQL / MariaDB
* **Front-end:** HTML5, CSS3 (variáveis CSS, layout responsivo)
* **Extensões PHP:** `GD` (manipulação de imagens), `mysqli` (comunicação com MySQL)

## 📂 Estrutura do Projeto

```text
.
├── bd.sql               # Script SQL de criação do banco de dados e tabelas
├── conexao.php          # Configuração de conexão com o banco e criação da pasta img/
├── geraSenha.php        # Utilitário CLI para geração de hashes bcrypt
├── valida_sessao.php    # Middleware/script de validação de login e sessão
├── login.php            # Tela e lógica de autenticação de usuários
├── logout.php           # Encerramento seguro de sessão
├── index.php            # Menu principal do sistema
├── cadastro_artista.php # CRUD completo de artistas + upload de fotos
├── cadastro_musica.php  # CRUD completo de músicas + capa + validação YouTube
├── listagem_musicas.php # Biblioteca musical com busca e filtros dinâmicos
├── styles.css           # Estilização global da aplicação
└── img/                 # Diretório de armazenamento das imagens enviadas (criado automaticamente)
```

## 🗄️ Modelo do Banco de Dados

O banco de dados `sistema_musical_v2` é composto por 3 tabelas principais:

1. **`usuarios`**: Armazena credenciais do sistema (`usuario`, `senha` em hash).
2. **`artistas`**: Armazena os dados dos artistas (`nome`, `genero`, `pais`, `imagem`).
3. **`musicas`**: Armazena os detalhes das faixas (`artista_id`, `titulo`, `album`, `genero`, `youtube_link`, `letra`, `imagem_capa`).

## 📝 Licença

Este projeto foi desenvolvido para fins educacionais e de prática em desenvolvimento web backend com PHP e MySQL. Sinta-se livre para utilizar, modificar e contribuir!
