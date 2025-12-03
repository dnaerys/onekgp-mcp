# 1000 Genomes Project dataset MCP Server

Natural language access to _**1000 Genomes Project dataset**_, hosted online in
_[Dnaerys variant store](https://dnaerys.org/)_
 

Dataset is sequenced & aligned to GRCh38 by _New York Genome Center_
- 2504 unrelated samples from the phase three panel
- additional 698 samples, related to samples in the 2504 panel
    - 3202 samples total (1598 males, 1604 females)
- [dataset details](https://www.internationalgenome.org/data-portal/data-collection/30x-grch38) 

### Key Features

- _real-time_ access to _138 044 724_ unique variants and about _442 billion_ individual genotypes in 3202 samples

- variant, sample, and genotype selection based on coordinates, annotations, zygosity

- filtering by VEP, ClinVar, gnomAD AF and AlphaMissense annotations
  
- filtering by inheritance model (de novo, heterozygous dominant, homozygous recessive)

## Deployments

Remote MCP service is available online via _Streamable HTTP:_

- http://db.dnaerys.org:80/mcp
- https://db.dnaerys.org:443/mcp

For local build with _stdio_ transport see [details below](https://github.com/dnaerys/onekgp-mcp/?tab=readme-ov-file#installation)

## Architecture

MCP Server is implemented as a Java EE service, accessing _1KGP dataset_ via gRPC API calls
to public _Dnaerys variant store_ service with _1000 Genomes dataset_ hosted online.

- service implementation is based on [Quarkus MCP Server](https://docs.quarkiverse.io/quarkus-mcp-server/dev/)
- provides MCP over _Streamable HTTP_, _HTTP/SSE_ and _STDIO_ transports


## Examples

Try analytical or open-ended questions to leverage analytical strength of LLMs, e.g.

> _Identify potential modifier variants for well-known pathogenic alleles in TTN - variants that consistently co-occur
in the same haplotype block with pathogenic alleles and may alter severity or penetrance. Conduct research for pathogenic
alleles documented in the literature. Use KGP dataset of healthy individuals to find potential modifier variants. Start with 100kb for
"the same haplotype block" definition, then extend if required. Evaluate statistical significance for the best modifier candidates found.
No initial constraints for modifier types._

- results might be _[some](https://claude.ai/public/artifacts/0185184c-96c6-4b2d-b1e3-d0d31a2c63df?fullscreen=true)_ _(Sonnet 4.5)_
- same task for _[KCNH2](https://claude.ai/public/artifacts/76761984-e06f-4fd9-9756-985692368cf9?fullscreen=true)_,
_[SCN5A](https://claude.ai/public/artifacts/f7930887-37cb-4174-b1db-7408eff0780f?fullscreen=true)_,
_[CACNA1C](https://claude.ai/public/artifacts/e857caf7-da6d-43f3-a8b7-36722a89f728?fullscreen=true)_, 
_[LMNA](https://claude.ai/public/artifacts/f12146e4-d9cc-48e3-9918-98d20796af6b?fullscreen=true)_ and
_[SPAST](https://claude.ai/public/artifacts/18ab99c2-d059-4592-969a-90c031290f8b?fullscreen=true)_ _(Sonnet 4.5)_

or

> _In what cardiac related genes, e.g. ion channels, variants in KGP dataset near catalytic residues or
   ligand-binding pockets show strong depletion compared to flanking residues (±20 amino acids) ?_
   
- results might be [some](https://claude.ai/public/artifacts/e81fa694-7de5-4fed-b903-e6cb23d02dd9?fullscreen=true) _(Sonnet 4.5)_

or

> _Are there patterns of variation in KGP dataset that suggest digenic or oligogenic interactions for Bardet-Biedl syndrome ?
   Check variety of combinations and zygosity patterns._

or

> _Which variants in the HBB gene are unexpectedly tolerated in the KGP dataset with at least several annotation sources
   in agreement with regard to their expected pathogenicity ?_

or

> _Rank all rare KGP variants in genes associated with arrhythmia disorder by their expected clinical relevance,
   not by predicted pathogenicity alone. Find affected individuals with highest clinical priority variants._

- results might be _[some](https://claude.ai/public/artifacts/c4fba7d9-545c-44ed-bc82-8c31a984e72a?fullscreen=true)_ _(Sonnet 4.5)_


_Feel free to open a PR with your favorite prompts_

## Available Tools

Description for 30 tools and parameters can be found [here](https://github.com/dnaerys/onekgp-mcp/blob/master/src/main/java/org/dnaerys/mcp/OneKGPMCPServer.java)

## Installation

Project can be run locally with MCP over _stdio_ transport, so the MCP server
can be started as a subprocess by MCP clients (like Claude Desktop or Goose).

- build the project and package it as a single _über-jar_:
    - jar is located in `target/onekgp-mcp-runner.jar` and includes all dependencies

```shell script
./mvnw clean
./mvnw package -DskipTests -Dquarkus.package.jar.type=uber-jar
```

- start from MCP client with a full path to the jar file (for _stdio_ transport,
  default configuration) or run as a separate service with streamable HTTP transport
  (requires a change in [configuration](https://github.com/dnaerys/onekgp-mcp/blob/master/src/main/resources/application.properties)) 
    - project expects _JRE 21_ to be available at runtime 

```shell script
java -jar <full path>/onekgp-mcp-runner.jar
```

#### Usage with Claude Desktop

To use with Claude Desktop, add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "OneKGP": {
      "command": "java",
      "args": ["-jar", "/full/path/onekgp-mcp-runner.jar"]
    }
  }
}
```

#### Verification

> How many variants exist in 1000 Genome Project ?


## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](https://github.com/dnaerys/onekgp-mcp/blob/master/LICENSE) file for details.
