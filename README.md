# Sistema de Logística e Cálculo de Frete

Atividade de **Desenvolvimento Back-End** em Java, criada para praticar programação orientada a objetos por meio de um sistema de logística com diferentes modalidades de transporte.

A aplicação funciona no terminal e calcula o **valor do frete** e o **prazo estimado de entrega** para caminhões e aviões de carga.

## Funcionalidades

- Informar os dados de um caminhão ou avião de carga.
- Calcular o frete conforme a modalidade, distância e peso.
- Estimar o prazo em horas com base na distância e velocidade média.
- Listar os fretes calculados durante a execução.
- Validar entradas numéricas positivas e impedir carga acima da capacidade informada.
- Validar combustível e tipo de carga no cadastro de caminhões.

## Modalidades e regras de cálculo

Considere **D** como distância em quilômetros e **P** como peso em quilogramas.

| Modalidade | Cálculo do frete |
| --- | --- |
| Transporte terrestre — base | `D × 0,50 + P × 0,10` |
| Caminhão | `(D × 0,50 + P × 0,10) × 1,20` |
| Transporte aéreo — base | `D × 0,80 + P × 0,30 + 150` |
| Avião de carga | `(D × 0,80 + P × 0,30 + 150) × 1,10` |

O caminhão aplica um acréscimo de **20%** sobre a base terrestre. O avião de carga aplica **10%** sobre a base aérea, que inclui um valor fixo de **R$ 150,00**.

O prazo das duas modalidades é calculado por:

```text
Prazo em horas = distância em km / velocidade média em km/h
```

Os valores são regras didáticas do exercício e não representam uma tabela comercial de fretes.

### Exemplo

Para uma distância de **100 km**, carga de **200 kg** e velocidade média de **50 km/h**:

| Modalidade | Frete | Prazo |
| --- | --- | --- |
| Caminhão | R$ 84,00 | 2 horas |
| Avião de carga | R$ 319,00 | 2 horas |

O exemplo usa a mesma velocidade para demonstrar a fórmula. Na utilização, cada veículo recebe sua própria velocidade média. A capacidade informada deve ser igual ou superior ao peso da carga.

## Conceitos de orientação a objetos

- **Encapsulamento:** atributos privados e acesso por getters e setters.
- **Herança:** modalidades específicas reutilizam atributos e comportamentos das classes superiores.
- **Sobrescrita de métodos:** `Caminhao` e `AviaoCarga` especializam o cálculo do frete.
- **Construtores e `super`:** inicialização dos atributos ao longo da hierarquia.
- **Coleções:** uso de `ArrayList` para armazenar transportes, fretes e prazos durante a sessão.
- **Tratamento de exceções:** leitura de dados com `Scanner` e tratamento de entradas inválidas.

## Organização do código

| Arquivo | Responsabilidade |
| --- | --- |
| [App.java](src/App.java) | Menu, entrada de dados, validações e listagem dos resultados |
| [Transporte.java](src/Transporte.java) | Dados comuns: capacidade, velocidade, distância e peso |
| [TransporteTerrestre.java](src/TransporteTerrestre.java) | Eixos, combustível e cálculo terrestre |
| [Caminhao.java](src/Caminhao.java) | Tipo de carga e acréscimo de 20% no frete |
| [TransporteAereo.java](src/TransporteAereo.java) | Altitude máxima, taxa de segurança e cálculo aéreo |
| [AviaoCarga.java](src/AviaoCarga.java) | Autonomia e acréscimo de 10% no frete |

Hierarquia: `Transporte → TransporteTerrestre → Caminhao` e `Transporte → TransporteAereo → AviaoCarga`.

## Como executar

Requisitos: **JDK** instalado, com `java` e `javac` disponíveis no PATH, e Git para clonar o repositório. O projeto utiliza a biblioteca padrão do Java, sem dependências externas.

```bash
git clone https://github.com/FelipeAugust0/sistema-logistica-java.git
cd sistema-logistica-java
```

Compile os arquivos a partir da raiz do projeto:

```bash
javac -encoding UTF-8 -d bin src/App.java src/Transporte.java src/TransporteTerrestre.java src/Caminhao.java src/TransporteAereo.java src/AviaoCarga.java
java -cp bin App
```

Também é possível abrir o projeto no VS Code com suporte a Java e executar o método `main` de `App.java`.

### Menu

```text
1 - Adicionar Caminhão
2 - Adicionar Avião de Carga
3 - Listar Fretes já calculados
0 - Sair
```

No caminhão, os combustíveis aceitos são `diesel`, `gasolina` e `etanol`; os tipos de carga são `seca` e `refrigerada`.

A leitura de números decimais segue a configuração regional do Java. Caso um valor seja rejeitado, confira se o ambiente espera vírgula ou ponto como separador decimal.

## Escopo e limitações

- Os dados ficam em memória e são perdidos ao encerrar o programa.
- A interface é de console; o projeto não expõe uma API HTTP nem utiliza banco de dados.
- Combustível, quantidade de eixos, tipo de carga, altitude e autonomia são armazenados, mas não alteram as fórmulas atuais.
- A taxa de segurança é um atributo da classe aérea, mas o cálculo utiliza o valor fixo de R$ 150,00. No menu atual, o construtor do avião recebe o peso também no parâmetro da taxa; esse atributo não participa do resultado.
- O prazo considera somente distância e velocidade, sem paradas, carregamento ou validação da autonomia do avião.

## Autor

Felipe Augusto da Silva — atividade acadêmica de Desenvolvimento Back-End.
