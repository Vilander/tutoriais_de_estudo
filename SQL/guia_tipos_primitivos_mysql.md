
# 📘 Guia dos Tipos Primitivos do MySQL

## 🔍 O que é um Tipo Primitivo?
Em bancos de dados, **tipos primitivos** (ou tipos de dados) definem **o tipo de valor que uma coluna pode armazenar**.  
No MySQL, isso garante que os dados sejam armazenados corretamente, ocupando o espaço certo e permitindo operações adequadas (como cálculos em números ou comparações de datas).

---

## 🔢 1. Tipos Numéricos
Usados para armazenar números (inteiros, decimais ou valores lógicos).

### 🔸 Inteiros
| Tipo | Tamanho aproximado | Uso |
|------|-------------------|-----|
| `TINYINT` | 1 byte (-128 a 127) | Números pequenos (flags, status). |
| `SMALLINT` | 2 bytes (-32.768 a 32.767) | Valores inteiros pequenos. |
| `MEDIUMINT` | 3 bytes | Valores inteiros médios. |
| `INT` ou `INTEGER` | 4 bytes (-2bi a 2bi) | Valores inteiros padrão. |
| `BIGINT` | 8 bytes | Números muito grandes. |

```sql
CREATE TABLE produtos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    estoque SMALLINT NOT NULL
);
```

---

### 🔸 Reais (decimais e ponto flutuante)
| Tipo | Uso |
|------|-----|
| `DECIMAL(p, s)` | Número exato com precisão. `p`=total de dígitos, `s`=decimais. |
| `FLOAT` | Número aproximado com 4 bytes. |
| `DOUBLE` ou `REAL` | Número aproximado com 8 bytes. |

```sql
CREATE TABLE pedidos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    valor_total DECIMAL(10, 2) NOT NULL
);
```

---

### 🔸 Lógicos
| Tipo | Uso |
|------|-----|
| `BIT` | Armazena bits (0 ou 1). |
| `BOOLEAN` ou `BOOL` | Aceita `TRUE` ou `FALSE`. |

```sql
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    ativo BOOLEAN DEFAULT TRUE
);
```

---

## ⏳ 2. Tipos de Data e Tempo
Usados para armazenar datas, horas e períodos.

| Tipo | Uso |
|------|-----|
| `DATE` | Apenas data (`YYYY-MM-DD`). |
| `DATETIME` | Data e hora (`YYYY-MM-DD HH:MM:SS`). |
| `TIMESTAMP` | Igual ao `DATETIME`, mas em UTC e atualiza automaticamente. |
| `TIME` | Apenas hora (`HH:MM:SS`). |
| `YEAR` | Ano com 4 dígitos. |

```sql
CREATE TABLE eventos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    data_evento DATE NOT NULL,
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🔤 3. Tipos Literais (Texto, Binário e Coleção)

### 🔸 Caractere (Strings curtas)
| Tipo | Uso |
|------|-----|
| `CHAR(n)` | Texto fixo (mesmo tamanho para todos). |
| `VARCHAR(n)` | Texto variável, até `n` caracteres. |

```sql
CREATE TABLE clientes (
    nome VARCHAR(100) NOT NULL
);
```

---

### 🔸 Texto (Strings longas)
| Tipo | Tamanho máximo |
|------|----------------|
| `TINYTEXT` | 255 caracteres |
| `TEXT` | 65.535 caracteres |
| `MEDIUMTEXT` | 16 milhões |
| `LONGTEXT` | 4 bilhões |

```sql
CREATE TABLE artigos (
    titulo VARCHAR(255),
    conteudo LONGTEXT
);
```

---

### 🔸 Binário
| Tipo | Tamanho máximo |
|------|----------------|
| `TINYBLOB` | 255 bytes |
| `BLOB` | 65 KB |
| `MEDIUMBLOB` | 16 MB |
| `LONGBLOB` | 4 GB |

```sql
CREATE TABLE arquivos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    dados LONGBLOB
);
```

---

### 🔸 Coleção
| Tipo | Uso |
|------|-----|
| `ENUM` | Lista de valores fixos. |
| `SET` | Lista de valores onde múltiplos podem ser escolhidos. |

```sql
CREATE TABLE produtos (
    tamanho ENUM('P', 'M', 'G', 'GG'),
    cores SET('vermelho', 'azul', 'verde')
);
```

---

## 📍 4. Tipos Espaciais (Geográficos)
Usados para armazenar dados de mapas, coordenadas e formas.

| Tipo | Uso |
|------|-----|
| `GEOMETRY` | Qualquer tipo geométrico. |
| `POINT` | Um ponto (latitude/longitude). |
| `POLYGON` | Um polígono. |
| `MULTIPOLYGON` | Vários polígonos. |

```sql
CREATE TABLE localidades (
    id INT AUTO_INCREMENT PRIMARY KEY,
    coordenadas POINT
);
```

---

## 📝 Resumo:
- **Numérico:** Inteiros, reais, booleanos.  
- **Data/Tempo:** Datas e horários.  
- **Literal:** Texto, binário, coleções.  
- **Espacial:** Dados geográficos.
