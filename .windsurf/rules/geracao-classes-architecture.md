---
trigger: model_decision
description: 
globs: 
---

# Regras de geração de classes

Este guia orienta a IA a criar novas classes e módulos respeitando a estrutura, convenções e camadas atuais do projeto.

## Pacote base
- **com.algaworks.algasensors**, o que vem em seguida define o microsserviço

## Camadas e diretórios (`com/algaworks/algasensors/device/management`)

- **(raiz) `device.management`**
  - Bootstrap da aplicação Spring Boot.
  - Exemplo: `DeviceManagementApplication`.
- **`api`**
  - Camada de entrada HTTP (REST), contratos de request/response e configurações de serialização/conversão para a API.
  - Subpacotes atuais: `config`, `controller`, `model`.
- **`api/config`**
  - Configurações técnicas da camada web/API (Jackson, JPA converter e conversores MVC).
  - Subpacotes atuais: `jackson`, `jpa`, `web`.
- **`api/config/jackson`**
  - Serialização de tipos TSID para JSON (string), garantindo formato consistente nas respostas.
  - Exemplos: `TSIDJacksonConfig`, `TSIDToStringSerializer`.
- **`api/config/jpa`**
  - Conversão de TSID para persistência (TSID <-> `Long`) via `AttributeConverter`.
  - Exemplo: `TSIDToLongJPAAttributeConverter`.
- **`api/config/web`**
  - Conversão de parâmetros/path variables da web (`String` -> TSID) para uso nos controllers.
  - Exemplos: `WebConfig`, `StringToTSIDWebConverter`.
- **`api/controller`**
  - Endpoints REST de sensores (CRUD, paginação, status HTTP e mapeamento entre API e domínio).
  - Exemplo: `SensorController`.
- **`api/model`**
  - DTOs da API para entrada e saída dos endpoints, com validação de payload.
  - Exemplos: `SensorInput`, `SensorOutput`.
  
- **`common`**
  - Componentes utilitários compartilhados (neste pacote, geração de identificadores TSID).
  - Exemplo: `IdGenerator`.

- **`domain`**
  - Núcleo de negócio e persistência orientada ao domínio (entidades e contratos de repositório).
  - Subpacotes atuais: `model`, `repository`.
- **`domain/model`**
  - Modelo de domínio JPA (entidade `Sensor` e value object `SensorId`).
  - Exemplos: `Sensor`, `SensorId`.
- **`domain/repository`**
  - Abstrações de acesso a dados do domínio com Spring Data JPA.
  - Exemplo: `SensorRepository`.

## Convenções de nomes e anotações (`device.management`)

- **Application**
  - Classe principal com sufixo `Application` na raiz do pacote.
  - Anotação: `@SpringBootApplication`.
  - Exemplo: `DeviceManagementApplication`.

- **REST API (Controller)**
  - Classe com sufixo `Controller` em `api.controller`.
  - Anotações: `@RestController`, `@RequestMapping`, `@Validated`, `@RequiredArgsConstructor`.
  - Endpoints com `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping` e status com `@ResponseStatus` quando necessário.
  - Injeção por construtor via Lombok (`@RequiredArgsConstructor`) com dependências `final`.

- **Modelos da API (DTO)**
  - Classes em `api.model` com sufixos de intenção (`Input` para entrada, `Output` para saída).
  - `Input`: validação com Jakarta Bean Validation (ex.: `@NotNull`).
  - `Output`: montagem via builder (`@Builder`) para respostas.

- **Configuração Web / Serialização / Persistência**
  - Classes de configuração com sufixo `Config` em `api.config.*`.
  - Anotação: `@Configuration`.
  - Conversores/serializadores com nomes explícitos de transformação:
    - `StringToTSIDWebConverter` (`Converter<String, TSID>`) em `api.config.web`.
    - `TSIDToStringSerializer` (`JsonSerializer<TSID>`) em `api.config.jackson`.
    - `TSIDToLongJPAAttributeConverter` (`AttributeConverter<TSID, Long>`) em `api.config.jpa`, com `@Converter(autoApply = true)`.

- **Entidade de domínio**
  - Classe de entidade em `domain.model`.
  - Anotações: `@Entity`, `@Id`, `@Column`.
  - Uso de Lombok para modelo rico de dados (`@Data`, `@Builder`, `@NoArgsConstructor`, `@AllArgsConstructor`).
  - Exemplo: `Sensor`.

- **Value Object de Identificador**
  - Nome com sufixo `Id` em `domain.model`.
  - Anotação: `@Embeddable` e implementação de `Serializable`.
  - Encapsula TSID e oferece construtores por tipo (`TSID`, `Long`, `String`).
  - Exemplo: `SensorId`.

- **Repository**
  - Interface com sufixo `Repository` em `domain.repository`.
  - Convenção: `extends JpaRepository<Entidade, IdDoDominio>`.
  - Neste pacote não há anotação explícita `@Repository` (detecção automática pelo Spring Data).
  - Exemplo: `SensorRepository extends JpaRepository<Sensor, SensorId>`.

- **Utilitários compartilhados**
  - Classes utilitárias em `common` com método estático e construtor privado.
  - Nome orientado à responsabilidade.
  - Exemplo: `IdGenerator` para geração de TSID.

## Regras de dependência entre camadas (`device.management`)

- **`api` (presentation)**
  - Pode consumir `domain` e `common`.
  - Deve orquestrar HTTP, validação de entrada e mapeamento de modelos de API.
  - Neste serviço atual, o acesso a dados ocorre via `domain.repository` diretamente no controller.
  - Não deve ser consumida por `domain` nem por `common`.

- **`domain`**
  - Define modelo de negócio (`domain.model`) e contratos/acesso a persistência (`domain.repository`).
  - Não depende de `api`.
  - Pode usar tipos técnicos necessários ao domínio (ex.: JPA, TSID), preservando foco em regras e estado de negócio.

- **`common`**
  - Contém utilitários compartilhados e transversais (ex.: geração de IDs).
  - Pode ser consumida por `api` e `domain`.
  - Não deve depender de `api` nem de detalhes de fluxo HTTP.

- **`api.config` (infraestrutura técnica local da API)**
  - Centraliza configuração de framework (Web MVC, Jackson, JPA converters).
  - Pode depender de bibliotecas técnicas e tipos compartilhados (`TSID`), sem lógica de negócio.
  - Não define regras de domínio.

- **Direção permitida (resumo)**
  - `api` -> `domain`
  - `api` -> `common`
  - `domain` -> `common` (quando necessário)
  - `api.config` -> componentes técnicos/framework
  - Proibido: `domain` -> `api`, `common` -> `api`, e dependências circulares entre camadas.
