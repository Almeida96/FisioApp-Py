# FisioApp Python (Tkinter)

Este é um **sistema de gerenciamento de pacientes** em Python, utilizando **Tkinter** para a interface gráfica. Permite **cadastrar**, **editar**, **excluir** pacientes, bem como **registrar** e **visualizar** sessões. O aplicativo trabalha com **pacotes de 10 sessões**, mostrando quantas faltam para encerrar o pacote atual.

## Sumário
- [Descrição Geral](#descrição-geral)
- [Funcionalidades](#funcionalidades)
- [Pacotes de 10 Sessões](#pacotes-de-10-sessões)
- [Pré-Requisitos](#pré-requisitos)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Como Usar](#como-usar)
- [Exemplo de Execução](#exemplo-de-execução)
- [Observações](#observações)
- [Licença](#licença)

---

## Descrição Geral

O **FisioApp** salva os dados em um arquivo JSON (`pacientes.json`). Cada paciente possui:
- **ID** (gerado automaticamente),  
- **Nome**,  
- **Idade**,  
- **Diagnóstico** e  
- **Histórico de Sessões** (observações).

A interface gráfica é feita em **Tkinter**. Quando o programa inicia, é exibido um **alerta** caso algum paciente esteja a **1 ou 2 sessões** de terminar o pacote de 10.

---

## Funcionalidades

1. **Cadastrar Paciente**  
   - Gera um **ID automático** (o menor disponível) e permite inserir nome, idade e diagnóstico.

2. **Registrar Sessão**  
   - Informa observações sobre uma nova sessão para o paciente selecionado.

3. **Editar Paciente**  
   - Atualiza nome, idade e/ou diagnóstico.

4. **Excluir Paciente**  
   - Remove definitivamente o paciente.

5. **Listar Pacientes**  
   - Exibe todos os pacientes ordenados por ID, com **barra de rolagem** caso a lista seja extensa.

6. **Visualizar Histórico**  
   - Mostra todas as sessões do paciente em uma nova janela, **limitada a 10 linhas de altura** e com **scrollbar** para rolagem. Também informa:
     - **Total** de sessões realizadas.
     - **Quantas faltam** para encerrar o pacote atual (ex.: se o paciente já fez 23 sessões, ele concluiu 2 pacotes (20) e está 3 sessões no terceiro pacote, faltando 7 para chegar em 30).

7. **Sair**  
   - Fecha o programa.

---

## Pacotes de 10 Sessões

- Cada **pacote** contém **10 sessões**.  
- Se um paciente tem **N** sessões, o pacote atual é determinado por `N % 10`.  
  - Se `N % 10 == 0`, acabou de **encerrar** um pacote, e se continuar, inicia-se um **novo** pacote (então faltam 10).  
  - Se `N % 10 != 0`, faltam `10 - (N % 10)` para encerrar o pacote atual.

**Exemplo**:  
- Paciente fez **28** sessões no total. Ele completou **2** pacotes (20) e está **8** sessões no pacote atual. Portanto, faltam **2** sessões para fechar **30**.

---

## Pré-Requisitos

- Python 3 instalado (Tkinter já vem incluso na maior parte das instalações padrão).  
- Qualquer sistema operacional compatível (Windows, Linux, macOS).

---

## Estrutura do Projeto

```
FisioAppPython
├── main.py
└── pacientes.json  (criado automaticamente se não existir)
```

- **`main.py`**: Código-fonte principal, contendo:
  - Definição das funções de persistência em JSON.
  - Classe `FisioApp` (com todos os métodos para cadastrar, listar, etc.).
  - Função que gera IDs automáticos.
- **`pacientes.json`**: Arquivo que armazena os pacientes e respectivos históricos.

> Se `pacientes.json` não existir ou estiver vazio, será **criado** na primeira execução.

---

## Como Usar

1. **Obtenha** o arquivo `main.py`.  
2. **Abra** um terminal na mesma pasta do `main.py`.
3. Execute:
   ```bash
   python main.py
   ```
   ou (em alguns sistemas):
   ```bash
   python3 main.py
   ```
4. Aparecerá uma janela principal com botões para cada ação (cadastrar paciente, registrar sessão, etc.).

---

## Exemplo de Execução

- **Ao abrir o programa**: Se houver pacientes a 1 ou 2 sessões de encerrar o pacote de 10, aparece uma **janela** alertando:
  ```
  Pacientes próximos de encerrar o pacote:
   - ID 2: Maria (faltam 2 sessões)
  ```
- **Cadastrar Paciente**:
  - Gera ID automático (ex.: se há IDs 1, 2 e 4, o próximo será 3).
  - Informa nome, idade, diagnóstico e salva em `pacientes.json`.
- **Visualizar Histórico**:
  - Informa quantas sessões já foram realizadas (ex.: 15) e quantas faltam (5 para fechar 20).
  - Exibe até 10 linhas com scroll, permitindo ver todas as sessões sem a janela ficar muito grande.

---

## Observações

- Caso o **arquivo JSON** fique corrompido, o sistema inicia com dados vazios e mostra um aviso.
- A **barra de rolagem** é utilizada tanto para **Listar Pacientes** (se a lista for extensa) quanto para o **Histórico** (se o paciente tiver mais de 10 sessões).
- Pode-se **personalizar** a lógica de pacotes (por exemplo, pacotes de 15 ou 20 sessões).
- Se não quiser ver o alerta de quem faltam 1 ou 2 sessões, basta remover ou comentar a função `alerta_pacientes_proximos_fim()` no construtor.

---
