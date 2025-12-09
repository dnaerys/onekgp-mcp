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

For local build with _stdio_ transport see [details below](https://github.com/dnaerys/onekgpd-mcp/?tab=readme-ov-file#installation)

## Architecture

MCP Server is implemented as a Java EE service, accessing _1KGP dataset_ via gRPC calls to public Dnaerys variant store service.

- service implementation is based on [Quarkus MCP Server](https://docs.quarkiverse.io/quarkus-mcp-server/dev/)
- provides MCP over _Streamable HTTP_, _HTTP/SSE_ and _STDIO_ transports


## Examples

Answers below are from _Sonnet 4.5_: some from _[multi-agent Research system](https://www.anthropic.com/engineering/multi-agent-research-system)_,
some with _extended thinking mode_, and some from a single-agent system in normal mode.  


#### Incomplete Penetrance & Genetic Resilience

> _Identify potential modifier variants for well-known pathogenic alleles in TTN - variants that consistently co-occur
in the same haplotype block with pathogenic alleles and may alter severity or penetrance. Conduct research for pathogenic
alleles documented in the literature. Use KGP dataset of healthy individuals to find potential modifier variants. Start with 100kb for
"the same haplotype block" definition, then extend if required. Evaluate statistical significance for the best modifier candidates found.
No initial constraints for modifier types._

- it feels a bit unreal how easily this thing can pull _[not entirely nonsensical](https://claude.ai/public/artifacts/13684418-36b2-4640-8ad6-5156b933eed9?fullscreen=true)_
events from a dataset with p = 2.29×10⁻¹³ (full [report](https://claude.ai/public/artifacts/864f857f-9018-4305-b5f0-e1095542547a?fullscreen=true)
and [visualisation](https://github.com/user-attachments/assets/3a6722d9-6d42-47cf-815b-d354669977a3) attempt)...
which makes one wonder what else is possible with a proper study design, specialised disease and
[control](https://www.nature.com/articles/s41467-019-14079-0) cohorts, and a bit more dedication
- same task for _[KCNH2](https://claude.ai/public/artifacts/76761984-e06f-4fd9-9756-985692368cf9?fullscreen=true)_,
_[SCN5A](https://claude.ai/public/artifacts/f7930887-37cb-4174-b1db-7408eff0780f?fullscreen=true)_,
_[CACNA1C](https://claude.ai/public/artifacts/e857caf7-da6d-43f3-a8b7-36722a89f728?fullscreen=true)_,
_[LMNA](https://claude.ai/public/artifacts/f12146e4-d9cc-48e3-9918-98d20796af6b?fullscreen=true)_,
_[SPAST](https://claude.ai/public/artifacts/18ab99c2-d059-4592-969a-90c031290f8b?fullscreen=true)_ and
_[BMPR2](https://claude.ai/public/artifacts/7163af75-20aa-41d4-8828-6accd7dc97f2?fullscreen=true)_

> _Select samples carrying known dominant-negative variants in KRT5 or KRT14 genes (Epidermolysis Bullosa) in the KGP.
Search for potential cis- or trans-acting rescue modifiers. Specifically, check if these samples carry variants that promote
the upregulation of the homologous KRT6 or KRT16 genes (paralog compensation). Can you detect a statistically significant
enrichment of 'paralog-boosting' promoter variants in these resilient carriers ?_

- [summary](https://claude.ai/public/artifacts/999d73dd-7b28-47ea-90f1-62be182b15a8), 
[report](https://claude.ai/public/artifacts/95b19c53-1864-4ebc-af48-f9f9bf50f9d2),
[fig 1](https://github.com/user-attachments/assets/b25fbe94-cd4b-40c6-95da-a080030f8b25),
[fig 2](https://github.com/user-attachments/assets/1c7df16f-6b0a-40ce-8712-042e2f14c182),
[fig 3](https://github.com/user-attachments/assets/76b05924-f949-4c96-9fc3-23fd042b88b6)

> _Which variants in the HBB gene are unexpectedly tolerated in the KGP dataset with at least several annotation sources
   in agreement with regard to their expected pathogenicity ?_

#### Structural Intolerance

> _Which regions in POLR2A are most likely disease-critical, with strong purifying selection, based on available
variation patterns across functional domains in KGP ? Do statistical evaluation._

- results for [CACNA1A](https://claude.ai/public/artifacts/9707df35-ceea-4cb1-a54d-0c392db3c38c?fullscreen=true) ([chart](https://github.com/user-attachments/assets/0e568973-5690-4334-abb9-833808d1fce9)),
[SCN1A](https://claude.ai/public/artifacts/7ce01d30-9bbc-4823-9be5-4d20f51137e1?fullscreen=true),
[SCN2A](https://claude.ai/public/artifacts/9be55bf0-c38f-4aba-bfd3-4361463b713b?fullscreen=true) ([chart](https://github.com/user-attachments/assets/9c1d6c6b-55b7-41a2-be85-b0f9fde08c68)), 
[POLR2A](https://claude.ai/public/artifacts/eeaa2483-a7ca-4f4e-81c3-e9ea435bd438?fullscreen=true) ([chart](https://github.com/user-attachments/assets/7df15795-351b-4066-8a81-fd3f98134f08)), 
[RPL5](https://claude.ai/public/artifacts/75f05627-75e2-4826-a2f0-13d2bd05e7e7?fullscreen=true) ([interactive vis](https://claude.ai/public/artifacts/a7baecef-83e7-463f-a2cf-0dfee441e24a)),
[RPL11](https://claude.ai/public/artifacts/f3fe732b-671b-48f9-956a-439d2d46698b?fullscreen=true),
[RPS26](https://claude.ai/public/artifacts/50c82a35-427e-494c-ab30-8b03b8dafc7c?fullscreen=true)


> _In what cardiac related genes, e.g. ion channels, variants in KGP dataset near catalytic residues or
ligand-binding pockets show strong depletion compared to flanking residues (±20 amino acids) ?_
   
- results might be [some](https://claude.ai/public/artifacts/e81fa694-7de5-4fed-b903-e6cb23d02dd9?fullscreen=true)


#### VUS Reclassification & AlphaMissense Integration

> _Retrieve all variants in KGP dataset in the voltage-gated sodium channel gene family (SCN1A, SCN2A, SCN5A)
currently classified as 'VUS' in ClinVar. Correlate their 'Likely Pathogenic' AlphaMissense classification
with their frequency in this healthy cohort. Synthesize a reasoned argument to reclassify a subset of these
as 'Likely Benign' based on the logic that pathogenic predictions by AlphaMissense are incompatible with the
observed allele frequency in this healthy population._

- [summary](https://claude.ai/public/artifacts/9a602e37-6795-4979-8b8c-48b052b33501?fullscreen=true),
[report](https://claude.ai/public/artifacts/3888c6d2-9b6d-435c-88f3-fde159e5b241?fullscreen=true),
[variants](https://claude.ai/public/artifacts/f9b6557b-c1e1-414f-ae1c-d62d256cb46a?fullscreen=true)

> _Analyze the distribution of missense variants in the BRCA1 and BRCA2 genes found in the KGP dataset. Map these variants
to the 3D protein structures (using your internal knowledge). Identify specific structural domains (e.g. the BRCT domain vs.
unstructured loops) that tolerate a high density of AlphaMissense-predicted 'ambiguous' variants in this healthy cohort,
effectively creating a 'map of benign tolerance' for future clinical reference._

- [summary](https://claude.ai/public/artifacts/b06a5d2a-45cf-4a55-b045-f453d52b47c7?fullscreen=true),
[report](https://claude.ai/public/artifacts/004375b5-76c6-43b1-9793-05f75ca993b2?fullscreen=true),
[variants](https://claude.ai/public/artifacts/fda1f207-0002-4a22-be11-37f2634f9f75?fullscreen=true),
[ASCII art](https://claude.ai/public/artifacts/36818f98-19fe-4df4-8067-87ee33cac703?fullscreen=true)


#### Oligogenic Signatures

> _Are there patterns of variation in KGP dataset that suggest digenic or oligogenic interactions for Bardet-Biedl syndrome ?
Check variety of combinations and zygosity patterns._


#### Protein-Protein Interactions

> _Analyze samples in the KGP dataset with missense variants located at the 'hinge' or 'head' domains in Cohesin complex genes
(SMC1A, SMC3, RAD21). Perform a 'co-evolution' analysis - do samples with a destabilizing mutation in the SMC1A head domain
tend to carry a complementary variant in the SMC3 head domain that restores electrostatic compatibility (e.g., a charge swap
from Glu->Lys in one and Lys->Glu in the other) ?_

- results might be _[some](https://claude.ai/public/artifacts/ea605022-296d-446d-989f-a9e7bae5ab6b)_


_Feel free to open a PR with your favorite prompts_

## Available Tools

Description for 30 tools and parameters can be found [here](https://github.com/dnaerys/onekgpd-mcp/blob/master/src/main/java/org/dnaerys/mcp/OneKGPMCPServer.java)

## Installation

Project can be run locally with MCP over _stdio_ transport, so the MCP server
can be started as a subprocess by MCP clients (e.g. Claude Desktop, [Goose](https://github.com/block/goose)
or [others](https://github.com/punkpeye/awesome-mcp-clients)).

- build the project and package it as a single _über-jar_:
    - jar is located in `target/onekgpd-mcp-runner.jar` and includes all dependencies

```shell script
./mvnw clean
./mvnw package -DskipTests -Dquarkus.package.jar.type=uber-jar
```

- start from MCP client with a full path to the jar file (for _stdio_ transport,
  default configuration) or run as a separate service with streamable HTTP transport
  (requires a change in [configuration](https://github.com/dnaerys/onekgpd-mcp/blob/master/src/main/resources/application.properties)) 
    - project expects _JRE 21_ to be available at runtime 

```shell script
java -jar <full path>/onekgpd-mcp-runner.jar
```

#### Usage with Claude Desktop

To use with Claude Desktop, add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "OneKGPd": {
      "command": "java",
      "args": ["-jar", "/full/path/onekgpd-mcp-runner.jar"]
    }
  }
}
```

#### Verification

> How many variants exist in 1000 Genome Project ?


## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](https://github.com/dnaerys/onekgpd-mcp/blob/master/LICENSE) file for details.
